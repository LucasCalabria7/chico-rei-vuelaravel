
<script>
export default {
    name: "Card",
    props: {
        dadosProduto: {
            type: Object,
            required: true,
        },
    },
};
</script>

<template>
    <div>
        <div id="global-card">
            <div id="image-area">
                <img id="card-image" :src="dadosProduto.images[0]" alt="card-image" />
                <div id="title-area">
                    <p id="card-title">{{ dadosProduto.title }}</p>
                    <button id="add-button">Adicionar</button>
                </div>
            </div>
            <div id="info-area">
                <p><i><b>{{ dadosProduto.brand }}</b></i></p>
                <h4 id="price">R${{ dadosProduto.price }}</h4>
                <div id="rating-area">
                    <img id="rating-icon" src="../assets/rating.png" />
                    <p id="rate">{{ dadosProduto.rating }}</p>
                </div>
                <p id="description">{{ dadosProduto.description }}</p>
            </div>
        </div>
    </div>
</template>

<style scoped>
#global-card {
    width: 32rem;
    height: 22rem;
    box-shadow: 0px 0.25rem 0.60rem 0 #db7416;
    border-radius: 0.75rem;
    display: flex;
    gap: 1rem;
    overflow-y: hidden;
}

#image-area {
    width: 60%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: space-evenly;
    flex-direction: column;
    padding: 0.25rem;
    margin-top: 0.25rem;
}

#card-image {
    height: 65%;
    width: 100%;
    border-radius: 0.75rem;
}

#title-area {
    width: 85%;
    height: 85%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 1.25rem;
}

#card-title {
    font-weight: bold;
    font-size: 1.1rem;
}

#add-button {
    height: 4vh;
    width: 100%;
    color: white;
    background-color: rgb(255, 170, 59);
    border: none;
    cursor: pointer;
    font-weight: bold;
    border-radius: 0.75rem;
    transition: all 0.2s ease-in-out;
}

#add-button:hover {
    background-color: #f29000;
}

#info-area {
    width: 40%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-items: center;
    padding-top: 1rem;
}

#price {
    color: #db7416;
    font-size: 2rem;
}

#rating-area {
    display: flex;
    align-items: center;
    gap: 1rem;
    width: 100%;
    justify-content: center;
}

#rating-icon {
    height: 1.5rem;
}

#rate {
    font-style: italic;
}

#description {
    font-weight: bold;
    font-size: 0.9rem;
    padding-left: 0.65REM;
}
</style>