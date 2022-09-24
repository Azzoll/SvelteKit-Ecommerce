<ul>
    <li><h1><a href="/" id="store">My Fake Store</a></h1></li>
    <li><a href="/" class="t">Home</a></li>
    <li><a href="/about-us" class="t">About Us</a></li>
    <li><a href="/FAQ" class="t">FAQ</a></li>
    <li><a href="/shop" class="t">Shop</a></li>
</ul>


<main><slot></slot></main>

<style>
    :global(body){
        font-family: 'Montserrat', sans-serif;;
    }
    * {
        padding: 0;
        margin: 0;
    }
    :global(body) {
        padding: 0;
        margin: 0;
    }
    ul {
        list-style-type: none;
        overflow: hidden;
        background-color: white;
        background-size: cover;
        border-bottom: solid black;
    }
    #store {
        float: right;
        color: black;
        padding-right: 50px;
        font-size: 50px;
        text-decoration: none;
        border-left: solid black;
        padding-left: 20px;
    }
    .t {
        float: left;
        display: block;
        color: black;
        text-align: center;
        padding: 14px 16px;
        text-decoration: none;
    }
    .t:hover {
        border: solid black;
        border-radius: 5px;
    }
    

</style>
