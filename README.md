<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Prueba de Firestore para los chicxs</title>

    <script src="https://www.gstatic.com/firebasejs/7.2.3/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/7.2.3/firebase-firestore.js"></script>
</head>
<body>
    
    <script>
        var docData = {
    stringExample: "Hello world!",
    booleanExample: true,
    numberExample: 3.14159265,
    dateExample: firebase.firestore.Timestamp.fromDate(new Date("December 10, 1815")),
    arrayExample: [5, true, "hello"],
    nullExample: null,
    objectExample: {
        a: 5,
        b: {
            nested: "foo"
        }
    }
};
db.collection("data").doc("one").set(docData).then(function() {
    console.log("Document successfully written!");
});
        // DOC: https://firebase.google.com/docs/firestore/quickstart?authuser=2

        // inicializa la librería de firebase, con los identificadores de nuestros proyectos en firebase.google.com
        firebase.initializeApp({
            apiKey: "AIzaSyCCda6VStoMfQBGnY3KjewkC3SaYtX5WPg",
            authDomain: "mi-primer-proyecto-6e74e.firebaseapp.com",
            projectId: "mi-primer-proyecto-6e74e"
        });
        // en este punto firebase está listo para ser usado

        // se crea un objeto "referencia" para poder darle instrucciones al firestore de nuestro proyecto
        var db = firebase.firestore();

        writeSomething = () => db.collection("users").add({
                first: "Cesar",
                last: "Lovelace",
                born: 1815,
                son: {
                    first: "Ado",
                    last: "Lovelace",
                    born: 1840
                }
            })
            .then(function(docRef) {
                console.log("Document written with ID: ", docRef.id);
            })
            .catch(function(error) {
                console.error("Error adding document: ", error);
            });

        readAll = () => db.collection("users").get().then((querySnapshot) => {
                querySnapshot.forEach((doc) => {
                    console.log(`${doc.id} => ${doc.data().first}`);
                });
            });
    </script>
    
</body>
    <button onclick="writeSomething()">Escribir</button>
    <button onclick="readAll()">Leer</button>
</html>
