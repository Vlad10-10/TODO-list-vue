<script setup>
</script>
<template>
    <div class="nav">
        <nav>
                <button type='submit' @click='openForm'>All Meetups</button>
                <button type='submit' @click='openLink1'>Add New Meetup</button>
                <button type='submit' @click='openLink2'>My Favorites</button>
        </nav>
    </div>
</template>
<style scoped>
div.nav {
    background-color: #2c3e50;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100vw;
    height: 5em;
    margin-bottom: 3em;
    overflow: hidden;
    padding: 0;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.25);
}

nav {
    padding: 1rem;
}

nav{
    display: flex;
    gap: 1rem;
    margin: 0;
    padding: 0;
}

button {
    margin: 0;
    height: 4.4em;
    width: 10em;
    display: flex;
    justify-content: center;
    align-items: center;
    transition: all 0.48s ease-in-out;
}

a {
    color: white;
    text-decoration: none;
    font-weight: bold;
}

button:hover {
    background-color: #334a61;
    cursor: pointer;
    box-shadow: 0px 5px 32px rgb(10, 30, 250);
    border-radius: 10px;
}

button.active:active {
    border: 1px solid white;
}

button:active {
    background-color: #2e5276b7;
    transform: scaleX(0.85) scaleY(0.78);
    box-shadow: 2px 5px 32px rgb(16, 107, 205);
    border-radius: 20px;
    transition: all 0.27s ease-in-out;
    filter: drop-shadow(0 0 2em #42b883aa);
}

/* button:active:nth-child(1) {
    background-color: #2e5276b7;
    transform: scaleX(0.94) scaleY(0.88);
    box-shadow: 2px 5px 32px rgb(16, 107, 205);
    border-radius: 20px;
    transition: all 0.53s ease-in-out;
    filter: drop-shadow(0 0 2em #42b883aa);
}

button:active:nth-child(2) {
    background-color: #2e5276b7;
    transform: scaleX(0.94) scaleY(0.88);
    box-shadow: 2px 5px 32px rgb(16, 107, 205);
    border-radius: 20px;
    transition: all 0.53s ease-in-out;
    filter: drop-shadow(0 0 2em #42b883aa);
}

button:active:nth-child(3) {
    background-color: #2e5276b7;
    transform: scaleX(0.94) scaleY(0.88);
    box-shadow: 2px 5px 32px rgb(16, 107, 205);
    border-radius: 20px;
    transition: all 0.53s ease-in-out;
    filter: drop-shadow(0 0 2em #42b883aa);
} */
</style>