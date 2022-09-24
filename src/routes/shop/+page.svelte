<script lang="ts">
    import { onMount } from 'svelte'

    function something() {
        // Script for all the buttons in the store
        const removeCartItemButtons = document.getElementsByClassName('btnRemove')
        console.log(removeCartItemButtons)
        for (let i = 0; i < removeCartItemButtons.length; i++) {
            let button = removeCartItemButtons[i]
            button.addEventListener('click', removeCartItem)
        }
        const quantityInputs = document.getElementsByClassName('cartQuantityInput')
        for (let i = 0; i < quantityInputs.length; i++) {
            const input = quantityInputs[i]
            input.addEventListener('change', quantityChanged)
        }
        const addToCartButtons = document.getElementsByClassName('addToCartButton')
        for (let i = 0; i < addToCartButtons.length; i++) {
            const cartButton = addToCartButtons[i]
            cartButton.addEventListener('click', addToCartClicked)
        }
        document.getElementsByClassName('btnPurchase')[0].addEventListener('click', purchaseClicked)

        // Functions so for the Script
        function purchaseClicked() {
            alert('Thank you for your purchase!')
            const cartItems = document.getElementsByClassName('cartItems')[0]
            while (cartItems.hasChildNodes()) {
                cartItems.removeChild(cartItems.firstChild)
            }
            updateCartTotal()
        }

        function addToCartClicked(event: any) {
            const button = event.target
            const product = button.parentElement
            const name = product.getElementsByClassName('productName')[0].innerText
            const price = product.getElementsByClassName('productPrice')[0].innerText
            const image = product.getElementsByClassName('productImage')[0].src
            addItemToCart(name, price, image)
            updateCartTotal()  
        }

        function addItemToCart(name: any, price: any, image: any) {
            const cartRow = document.createElement('div')
            cartRow.classList.add('cartRow')
            const cartItems = document.getElementsByClassName('cartItems')[0]
            const cartItemNames = cartItems.getElementsByClassName('cartItemTitle')
            for (let i = 0; i < cartItemNames.length; i++) {
                if (cartItemNames[i].innerHTML == name) {
                    alert('Already in cart!')
                    return
                }
            }
            const cartRowContent = `
            <div class="cartItem cartColumn">
                <img class="cartItemImage" src="${image}" alt="${name}">
                <span class="cartItemTitle">${name}</span>
            </div>
            <span class="cartPrice cartColumn">${price}</span>
            <div class="cartQuantity cartColumn">
                <input class="cartQuantityInput" type="number" value="1">
                <button class="btn btnRemove" type="button">REMOVE</button>
            </div>`
            cartRow.innerHTML = cartRowContent
            cartItems.append(cartRow)
            cartRow.getElementsByClassName('btnRemove')[0].addEventListener('click', removeCartItem)
            cartRow.getElementsByClassName('cartQuantityInput')[0].addEventListener('change', quantityChanged)
        }

        function quantityChanged(event: any) {
            const input = event.target
            if (isNaN(input.value) || input.value <= 0) {
                input.value = 1
            }
            updateCartTotal()
        }

        function removeCartItem(event: any) {
            const buttonClicked = event.target as HTMLInputElement
            buttonClicked?.parentElement?.parentElement?.remove()
            updateCartTotal()
        }

        function updateCartTotal() {
            const cartItemContainer = document.getElementsByClassName('cartItems')[0]
            const cartRows = cartItemContainer.getElementsByClassName('cartRow')
            let total = 0
            for (let i = 0; i < cartRows.length; i++) {
                const cartRow = cartRows[i]
                const priceElement = cartRow.getElementsByClassName('cartPrice')[0]
                const quantityElement = cartRow.getElementsByClassName('cartQuantityInput')[0] as HTMLInputElement
                const price = parseFloat(priceElement.innerHTML.replace('$', ''))
                const quantity = parseFloat(quantityElement.value)
                total = total + (price * quantity)
            }
            total = Math.round(total * 100) / 100
            document.getElementsByClassName('cartTotalPrice')[0].innerHTML = total + '$'
        }
    }
    onMount(something)
</script>
<link rel="stylesheet" href="src/style.css">

<div class="shopTitle">
    <h2 class="cartTitle">SHOP</h2>
</div>
<!-- Items for Sales -->
<section class="product">
    <img class="productImage" src="product/dog/kong-toy.jpg" alt="KONG Toy for dog" width="150px" height="150px">
    <h1 class="productName">Kong Toy</h1>
    <h2 class="productPrice">19.99$</h2>
    <button class="addToCartButton">Add to Cart</button>
</section>
<section class="product">
    <img class="productImage" src="product/dog/dog-bed.jpg" alt="Dog Bed" width="150px" height="150px">
    <h1 class="productName">Dog Bed</h1>
    <h2 class="productPrice">29.99$</h2>
    <button class="addToCartButton">Add to Cart</button>
</section>
<section class="product">
    <img class="productImage" src="product/dog/dog-cage.webp" alt="Dog Cage" width="150px" height="150px">
    <h1 class="productName">Dog Cage</h1>
    <h2 class="productPrice">49.99$</h2>
    <button class="addToCartButton">Add to Cart</button>
</section>
<section class="product">
    <img class="productImage" src="product/cat/fish-toy.jpg" alt="Fish Toy for Cats" width="150px" height="150px">
    <h1 class="productName">Fish Toy</h1>
    <h2 class="productPrice">14.99$</h2>
    <button class="addToCartButton">Add to Cart</button>
</section>
<section class="product">
    <img class="productImage" src="product/cat/cat-bed.jpg" alt="Cat Bed" width="150px" height="150px">
    <h1 class="productName">Cat Bed</h1>
    <h2 class="productPrice">27.99$</h2>
    <button class="addToCartButton">Add to Cart</button>
</section>
<section class="product">
    <img class="productImage" src="product/cat/carrier-cage.jpg" alt="Carrier Cage for Cats" width="150px" height="150px">
    <h1 class="productName">Carrier Cage</h1>
    <h2 class="productPrice">35.99$</h2>
    <button class="addToCartButton">Add to Cart</button>
</section>

<!-- Cart Section of the page -->
<section class="containerCart">
    <h2 class="cartTitle">CART</h2>
    <div class="cartRow">
        <span class="cartItem cartHeader cartColumn">ITEM</span>
        <span class="cartPrice cartHeader cartColumn">PRICE</span>
        <span class="cartQuantity cartHeader cartColumn">QUANTITY</span>
    </div>
    <div class="cartItems">
    <!-- This is where items go when add to cart button is clicked -->
    </div>
    <div class="cartTotal">
        <strong class="cartTotalTitle">Total</strong>
        <span class="cartTotalPrice">0$</span>
    </div>
    <button class="btn btnPurchase" type="button">PURCHASE</button>
</section>

