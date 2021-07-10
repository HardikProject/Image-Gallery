<script>
let isSelected = {
    selection: false,
    src: ''
};
let imgArray = new Array();

for (let i = 0; i < 11; i++) {
    imgArray[i] = `/images/${i+1}.jpg`
}
</script>

<div class="container">
    <h1>Image Gallery</h1>
    <div class="gallery">
        {#each imgArray as image,i}
        <img src={image} alt={`image ${i}`} on:click={()=>{
            isSelected.selection=!isSelected.selection;
            isSelected.src=image;
        }}
        >
        {/each}
    </div>
    {#if isSelected.selection}
    <div class="popUp" on:click={()=> {
        isSelected.selection = !isSelected.selection;
        isSelected.src = '';
    }} >
        <img src={isSelected.src} alt={`image PopUp`} >
    </div>
    {/if}

</div>

<style>
img {
    width: 320px;
    height: 300px;
    border-radius: 6px;
    cursor: pointer;
    object-fit: cover;
    display: block;
    margin: 0 auto;
    transition: transform 300ms;
}

img:hover {
    box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
    transform: translateY(-2px);
}

.container {
    max-width: 95vw;
    margin: 0 auto;
    padding: 10px 20px;
}

.gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
    grid-gap: 20px;
    margin: 0 auto;
    background-color: white;
    width: 100%;
    padding: 20px;
    border-radius: 10px;
}

.popUp {
    position: fixed;
    inset: 0;
    background: rgba(0, 0, 0, 0.9);
    display: flex;
    justify-content: center;
    align-items: center;
}
.popUp img{
    width: 60vw;
    height: 80%;
}
.popUp img:hover{
    box-shadow: none;
    transform: none;
}

@media screen and (max-width:840px){
    .popUp img{
    width: 100%;
    height: 60%;
    border-radius: 6px;
    object-fit: contain;
}
}
</style>
