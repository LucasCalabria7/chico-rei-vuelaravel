<template>
    <div>
        <div class="global-header">
            <img id="first-logo" src="../assets/first-logo.png" alt="firstlogo" />
            <h2 id="main-logo">Chico Rei</h2>
            <div id="contact-area">
                <h2><a id="contato" href="https://chicorei.com/" target="_blank">Contato</a></h2>
                <a href="https://www.instagram.com/chicorei/" target="_blank"><img id="insta-icon"
                        src="../assets/instagram-icon.svg" /></a>
                <a href="https://www.facebook.com/chicorei" target="_blank"><img id="face-icon"
                        src="../assets/facebook-icon.svg" /></a>
            </div>
        </div>
    </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Alkatra&display=swap');

.global-header {
    height: 10vh;
    max-width: 100vw;
    background-color: #f2efe9;
    box-shadow: 0px 4px #201f1e;
    display: flex;
    justify-content: space-around;
    align-items: center;
    padding: 2rem;
}

#first-logo {
    height: 4rem;
    width: 4rem;
}

#main-logo {
    color: #201f1e;
    font-family: 'Alkatra', cursive;
}

#contact-area {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    height: 10vh;
    width: 4rem;
}

#contato {
    color: #201f1e;
    cursor: pointer;
    text-decoration: none;
}

#insta-icon,
#face-icon {
    height: 1rem;
    width: 1rem;
    cursor: pointer;
    margin-top: 4px;
}
</style>