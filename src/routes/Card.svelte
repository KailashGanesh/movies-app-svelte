<script lang="ts">
    export let src: string;
    export let alt: string;
    export let title: string;
    export let desc: string;
</script>

<li>
    <img src={src} alt={alt} />
    <h2>{title}</h2>
    <p>{desc}</p>
</li>

<style>
    li {
        list-style: none;
        padding: 40px;
        border: 1px solid #eee;
        width: 200px;
        box-shadow: gray 0px 0px 10px;
        position: relative;
        min-height: 350px;
        max-height: 350px;
    }
    
    li img{
        max-width: 100%;
    }

    li p {
        visibility: hidden;
        overflow: hidden;
        transition: all 1s ease-in-out;
        position: absolute;
        padding: 20px;
        left: 0;
        top: 25%;
        color: transparent;
    }

    li:hover p {
        visibility: visible;
        background-color: #eee;
        top: 0;
        color: black;
    }

</style>