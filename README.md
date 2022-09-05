# Marketplace

<p>
My first journey into event-driven architectures<br>
this project aims to be a marketplace with high thoughput event streaming,<br>
It is solely focused on learning experience and is currently in it's very early stages<br>
</p>

<p>
The current objective is to deal with orders and to learn the ins and outs of Kafka<br>
</p>

## Architecture (AS-IS):

<img src="public/architecture_asis.png" alt="architecture">

#### Customer Client

<p>
Creates orders, queries for orders, and displays live order status through websocket<br>
Does not query for vendors or products, it's all hardcoded for now<br>
</p>

#### Marketplace API

<p>
Creates, updates, and queries database for orders, publishes new orders to the kafka bus, writes all orders created and updated to the websocket endpoint<br>
</p>

#### Vendor Edge Worker

<p>
Subscribes to the new orders topic, submits new orders to the Vendor Edge API, publishes order status updates received from the Vendor Edge API to their respective topics<br>
</p>

#### Vendor Edge API

<p>
Receives new orders from the Vendor Edge Worker and mocks order status updates from vendors with random timeouts<br>
In the future it will have an endpoints facing the vendor client so that the vendors can see new orders and update their status<br>
</p>

#### Order Notifier Worker

<p>
Subscribes to all order topics that track status updates and calls the Marketplace API to update order statuses<br>
</p>
