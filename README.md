# Dojo récap React + appels API

On vous fournit une API (faite maison) permettant de récupérer des photos de voyage. L'URL de l'API (que vous pouvez tester dans Postman ou dans votre navigateur) : <https://mytravelapi.herokuapp.com/photos>

Comme je suis sympa :innocent:, voici un exemple de ce qu'elle renvoie (bon ce sera plus lisible dans Postman) :

```json
{
  "results": [
    {
      "id": 1,
      "authorId": 1,
      "title": "Macchu Picchu - From above",
      "picture": {
        "small": "https://mytravelapi.herokuapp.com/img/small/macchu-picchu-from-above.jpg",
        "medium": "https://mytravelapi.herokuapp.com/img/medium/macchu-picchu-from-above.jpg"
      },
      "country": "Peru",
      "date": "2005-02-25",
      "tags": [
        "incas",
        "ancient civilizations"
      ]
    },
    {
      "id": 11,
      "authorId": 1,
      "title": "Macchu Picchu - Details of a construction",
      "picture": {
        "small": "https://mytravelapi.herokuapp.com/img/small/macchu-picchu-details.jpg",
        "medium": "https://mytravelapi.herokuapp.com/img/medium/macchu-picchu-details.jpg"
      },
      "country": "Peru",
      "date": "2005-02-25",
      "tags": [
        "incas",
        "ancient civilizations"
      ]
    },
    ... coupé pour abréger ...
  ],
  "page": 1,
  "totalPages": 3,
  "totalResults": 14,
  "next": "https://mytravelapi.herokuapp.com/photos?page=2"
}
```

Si vous regardez bien, dans l'objet renvoyé par l'API, il y a surtout `results` qui contient un tableau d'objets. Les autres champs permettent de savoir combien de données sont dispo en tout dans l'API.

## 1. Écrire un composant PhotoCard

Ecrivez un composant `PhotoCard` permettant d'afficher certaines données d'**une** photo :

- Son titre (champ `title`) que vous passerez via la props `title`,
- Le pays (`country`) que vous passerez via la props `country`,
- L'image de petite taille (`small` dans `image`) que vous passerez via la props `imageUrl`.

L'idée est ensuite de l'appeler. Pour cela vous allez prendre un des objets "en dur" dans le JSON ci-dessous, et en faire une constante. Par exemple, dans votre `App.jsx`, mettez :

```javascript
const samplePhoto = {
  id: 1,
  authorId: 1,
  title: 'Macchu Picchu - From above',
  picture: {
    small:
      'https://mytravelapi.herokuapp.com/img/small/macchu-picchu-from-above.jpg',
    medium:
      'https://mytravelapi.herokuapp.com/img/medium/macchu-picchu-from-above.jpg',
  },
  country: 'Peru',
  date: '2005-02-25',
  tags: ['incas', 'ancient civilizations'],
};
```

Puis dans le JSX, appelez `PhotoCard` en lui passant des props, en les prenant depuis `samplePhoto`.

## 2. Utiliser un tableau de photos et répéter `PhotoCard`

Remplacez `samplePhoto` par `samplePhotos` (au pluriel) et assignez-lui un tableau comme valeur :

```javascript
const samplePhotos = [
  {
    id: 1,
    authorId: 1,
    title: 'Macchu Picchu - From above',
    picture: {
      small:
        'https://mytravelapi.herokuapp.com/img/small/macchu-picchu-from-above.jpg',
      medium:
        'https://mytravelapi.herokuapp.com/img/medium/macchu-picchu-from-above.jpg',
    },
    country: 'Peru',
    date: '2005-02-25',
    tags: ['incas', 'ancient civilizations'],
  },
  {
    id: 11,
    authorId: 1,
    title: 'Macchu Picchu - Details of a construction',
    picture: {
      small:
        'https://mytravelapi.herokuapp.com/img/small/macchu-picchu-details.jpg',
      medium:
        'https://mytravelapi.herokuapp.com/img/medium/macchu-picchu-details.jpg',
    },
    country: 'Peru',
    date: '2005-02-25',
    tags: ['incas', 'ancient civilizations'],
  },
];
```

Puis utilisez `map` sur ce tableau pour répéter le composant `PhotoCard`.

## 3. Se préparer pour faire des appels API

Il va d'abord falloir transformer le composant `App` en classe !

Puis lui ajouter un constructeur, et y initialiser un state :

```javascript
this.state = {
  photos: [],
};
```

Ensuite, ajouter une méthode `fetchPhotos` : cette méthode va faire un appel à l'API.

Vous pouvez utiliser soit Fetch, soit Axios comme dans la quête React 07.

Si vous utilisez Fetch :

```javascript
const url = 'https://mytravelapi.herokuapp.com/photos';
fetch(url)
  .then((response) => response.json())
  .then((data) => {
    // data contient les données renvoyées par l'API
  });
```

Si vous utilisez Axios :

```javascript
const url = 'https://mytravelapi.herokuapp.com/photos';
axios
  .get(url)
  .then((response) => response.data)
  .then((data) => {
    // data contient les données renvoyées par l'API
  });
```
