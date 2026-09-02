<template>
    <div class="container">
        <h1>Movies List</h1>
        <div class="btn__container--sortMovies">
            <button
                @click="sortMoviesAsc"
                class="btn--sortASC">
                A->Z
            </button>
            <button
                @click="sortMoviesDesc"
                class="btn--sortDESC">
                Z->A
            </button>
        </div>
        <form
            class="input__container"
            @submit.prevent="addNewMovie">
            <input
                type="text"
                v-model="newMovie"
                placeholder="ajoutez votre film..." />
            <button class="btn--add">Ajouter</button>
        </form>
        <ul>
            <li
                v-for="movie in moviesList"
                :key="movie">
                {{ movie }}

                <button
                    @click="removeMovie(movie)"
                    class="btn--remove">
                    X
                </button>
            </li>
        </ul>
    </div>
</template>

<script setup>
    import { ref } from 'vue'

    const moviesList = ref([
        'Harry Potter 5',
        'Star Wars episode III',
        'Interstellar',
        'Lilo & Stitch',
    ])

    const newMovie = ref('')

    const count = ref(0)
    console.log(count, count.value)

    const addNewMovie = () => {
        if (newMovie.value.trim() !== '') {
            moviesList.value.push(newMovie.value)
        }
        newMovie.value = ''
    }

    const removeMovie = movieToDelete => {
        moviesList.value = moviesList.value.filter(m => m !== movieToDelete)
    }

    // Tri A -> Z
    const sortMoviesAsc = () => {
        moviesList.value.sort((a, b) => (b > a ? -1 : 1))
    }

    // Tri Z -> A
    const sortMoviesDesc = () => {
        moviesList.value.sort((a, b) => (a > b ? -1 : 1))
    }
</script>

<style>
    @import url(https://fonts.googleapis.com/css?family=Inter:100,200,300,regular,500,600,700,800,900,100italic,200italic,300italic,italic,500italic,600italic,700italic,800italic,900italic);

    @import url(https://fonts.googleapis.com/css?family=Poppins:100,100italic,200,200italic,300,300italic,regular,italic,500,500italic,600,600italic,700,700italic,800,800italic,900,900italic);

    html {
        font-family: Inter, sans-serif;
    }

    body {
        background-color: rgb(33, 23, 51);
    }
    .container {
        margin: 0 auto;
        width: 600px;
        padding: 20px;
    }

    h1 {
        font-family: Poppins, sans-serif;
        text-align: center;
        font-size: 3rem;
        background: linear-gradient(to right, crimson, pink);
        background-clip: text;
        color: transparent;
    }

    .input__container {
        display: flex;
        justify-content: center;
        padding: 20px;
        gap: 5px;
    }

    .input__container input {
        padding: 10px;
        border-radius: 500px;
        border: none;
        outline: none;
        box-shadow: 0px 1px 10px #222;
    }

    button.btn--add {
        width: 75px;
        padding: 10px;
        border-radius: 500px;
        background: rgb(31, 144, 237);
        border: 1px solid rgb(31, 144, 237);
        font-weight: bold;
        color: #f1f1f1;
        box-shadow: 0px 1px 10px #222;
    }

    li {
        list-style: none;
        font-size: 1.5rem;
        display: flex;
        justify-content: space-between;
        padding: 5px;
        color: #f1f1f1;
    }

    button.btn--remove {
        width: 30px;
        height: 30px;
        border-radius: 500px;
        padding: 10px;
        display: flex;
        justify-content: center;
        align-items: center;
        background: rgb(238, 44, 83);
        color: #f1f1f1;
        font-weight: bold;
        border: none;
        box-shadow: 0px 2px 5px #222;
        transition: 0.3s ease-in-out;
    }

    button.btn--remove:hover {
        background: rgb(249, 87, 120);
        transform: translateY(-2px);
    }
    .active {
        font-style: italic;
        font-weight: bold;
    }
    button {
        cursor: pointer;
    }

    .btn__container--sortMovies {
        width: 400px;
        margin: 0 auto;
        padding: 10px;
        display: flex;
        justify-content: space-evenly;

        button {
            padding: 10px;
            border: none;
            border-radius: 5px;
            transition: 0.3s ease-in-out;
            box-shadow: 0px 2px 8px #aaa;
        }

        button:hover {
            transform: translateY(-2px);
        }

        .btn--sortASC {
            background-color: rgb(236, 251, 21);
        }

        .btn--sortASC:hover {
            background-color: rgb(235, 252, 99);
        }

        .btn--sortDESC {
            background-color: rgb(241, 125, 24);
        }

        .btn--sortDESC:hover {
            background-color: rgb(246, 171, 58);
        }
    }
</style>
