<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Delivery App</title>
    <script type="module" src="https://cdn.jsdelivr.net/npm/@ionic/core/dist/ionic/ionic.esm.js"></script>
    <script nomodule src="https://cdn.jsdelivr.net/npm/@ionic/core/dist/ionic/ionic.js"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@ionic/core/css/ionic.bundle.css" />
    <link rel="stylesheet" href="price.css">
</head>
<body>
    <ion-app>
        <!-- Header -->
        <ion-header>
            <ion-toolbar id="header">
                <ion-title id="hTitle">Checkout Form</ion-title>
            </ion-toolbar>
        </ion-header>

        <ion-content class="ion-padding">
            <!-- <img class="food" src="https://st.depositphotos.com/46351542/52009/i/450/depositphotos_520099256-stock-photo-delivery-concept-truck-boxes-smartphone.jpg" alt="foodPic"> -->
            <ion-list color="primary">
                <ion-item>
                    <ion-label position="floating">Name</ion-label><br>
                    <ion-input id="name" placeholder="Enter Name" clear-input="true"></ion-input>
                </ion-item>

                <ion-item>
                    <ion-label position="floating">Product Name</ion-label><br>
                    <ion-input id="pname" placeholder="Enter Product Name" clear-input="true"></ion-input>
                </ion-item>

                <ion-item>
                    <ion-label position="floating">Price</ion-label><br>
                    <ion-input id="price" placeholder="Enter Price" type="number" clear-input="true"></ion-input>
                </ion-item>

                <ion-item>
                    <ion-select label="Discounted" id="discount" placeholder="Discounted or not" interface="popover">
                        <ion-select-option value="Yes">Yes</ion-select-option>
                        <ion-select-option value="No">No</ion-select-option>
                    </ion-select>
                </ion-item>

                <ion-item id="showDiscount" style="display: none;">
                    <ion-label position="floating">Discount</ion-label><br>
                    <ion-input id="disAmount" placeholder="Enter Discount" type="number" clear-input="true"></ion-input>
                </ion-item>
            </ion-list>

            <!-- Results -->
            <ion-card>
                <ion-card-header id="saved" style="display: none">
                    <ion-card-title id="receipt">-- Receipt --</ion-card-title>
                    <div>
                        <div class="info-row">
                            <ion-card-title>Name:</ion-card-title>
                            <ion-card-subtitle id="pangalan"></ion-card-subtitle>
                        </div>
                        <div class="info-row">
                            <ion-card-title>Product Name:</ion-card-title>
                            <ion-card-subtitle id="product"></ion-card-subtitle>
                        </div>
                        <div class="info-row">
                            <ion-card-title>Price:</ion-card-title>
                            <ion-card-subtitle id="presyo"></ion-card-subtitle>
                        </div>
                        <div class="info-row">
                            <ion-card-title>Discounted:</ion-card-title>
                            <ion-card-subtitle id="selection"></ion-card-subtitle>
                        </div>
                        <div class="info-row">
                            <ion-card-title>Discount Amount:</ion-card-title>
                            <ion-card-subtitle id="discounted"></ion-card-subtitle>
                        </div>
                        <div class="info-row" style="display: none;" id="remLabel">
                            <ion-card-title>Total Price:</ion-card-title>
                            <ion-card-subtitle id="remResult"></ion-card-subtitle>
                        </div>
                    </div><br>
                    <ion-card-header id="result" style="display: none"></ion-card-header>
                </ion-card-header>

                <ion-card-header id="notSaved" style="display: none" color="danger"></ion-card-header>
            </ion-card>
        </ion-content>

        <ion-footer>
            <ion-button expand="block" fill="outline" onclick="triggerMode()">SUBMIT ORDER</ion-button>
        </ion-footer>
    </ion-app>

    <script>
        // Toggle discount input visibility
        document.getElementById('discount').addEventListener('ionChange', toggleInput);

        function toggleInput() {
            let discount = document.getElementById('discount').value;
            let showDiscount = document.getElementById('showDiscount');
            
            if (discount === 'Yes') {
                showDiscount.style.display = 'block';
            } else {
                showDiscount.style.display = 'none';
            }
        }

        function triggerMode() {
            let name = document.getElementById('name').value;
            let pname = document.getElementById('pname').value;
            let price = parseFloat(document.getElementById('price').value);
            let discount = document.getElementById('discount').value;
            let disAmount = parseFloat(document.getElementById('disAmount').value);

            if (discount === 'Yes') {
                let disTotal = (disAmount / 100) * price;
                let remResult = price - disTotal;

                document.getElementById('pangalan').innerText = name;
                document.getElementById('product').innerText = pname;
                document.getElementById('presyo').innerText = price;
                document.getElementById('selection').innerText = discount;
                document.getElementById('discounted').innerText = `${disAmount}%`;
                document.getElementById('remResult').innerText = remResult;
                
                document.getElementById('result').innerText = "Here is your result";
                document.getElementById('result').style.display = 'block';

                document.getElementById('remLabel').style.display = "flex";
                document.getElementById('remResult').style.display = "block";
                document.getElementById('saved').style.display = "block";
                document.getElementById('notSaved').style.display = "none";
            } else {
                // Hide receipt and show "Invalid" message if "No" is selected
                document.getElementById('saved').style.display = "none";
                document.getElementById('remLabel').style.display = "none";
                document.getElementById('remResult').style.display = "none";
                document.getElementById('notSaved').innerText = "No discount applied.";
                document.getElementById('notSaved').style.display = "block";
            }
        }
    </script>
</body>
</html>
