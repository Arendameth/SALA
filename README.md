# SALA
Documentation for configuration and usage of San Andreas Logistical Association (SALA) bot.

## Setting up the bot
### 1- Inviting the bot
Invite the bot to your trucking discord server by using [this link](https://discord.com/api/oauth2/authorize?client_id=976183145374318683&permissions=76816&scope=bot).
By default, the bot will have the following permissions when invited to a new server:
- Manage Roles
- Manage Channels
- Read Messages/View Channels
- Send Messages
- Manage Messages
- Read Message History

It is **HIGHLY** recommended that the bot is given an administrative role to ensure that it doesn't run into any permissions issues.

### 2- Enabling Bot Functionality in Your Server

By default, the bot will not be operational in your server upon invitation. This is to ensure that the bot is exclusively utilized within active trucking groups, thus eliminating any performance issues that may arise from the unnecessary bot's usage in unrelated servers.

To activate the bot's functionality in your trucking discord server, You need to ping me (`@arendameth`) in the `#group-owners` channel within the official valrise server. **Only** group owners are authorized to request bot functionality for their servers. Direct messages from group members will not be considered for this purpose.

### 3- Setting up the channels
One of the first things you must set up are the tickets channel, receipts channel, and archive channel. Don't worry, they'll be fully explained later in the guide. In order to do that, you can use the command `/setchannel {channel_type} {channel}`. The strings accepted in `channel_type` parameters are explained below. Parameters are case sensitive. Make sure the bot always has the permission to write to those channels.
| Channel Type  | Information | Illustration |
| ------------- | ------------- | ------------- |
| ticketsChannel  | The channel which the `Create Ticket` button is sent to. | ![ticketsChannel illustration](https://i.ibb.co/PD8LZsK/image.png)
| receiptsChannel  | The channel which new trucking orders are sent to for truckers to claim. This channel is typically exclusive to staff only. | ![receiptsChannel illustration](https://i.ibb.co/KFDGnNY/image.png) |
| archiveChannel | The channel which transcripts of closed tickets are sent to. Typically exclusive to high ranks only. | ![archiveChannel illustration](https://i.ibb.co/71yVP24/image.png) |

### 4- Setting up the tickets category and company name
You need to set up which category new tickets will go to. By default, it will be `tickets`, so you need to ensure you already have a category called `tickets`. You can change it by using `/changesetting ticketsCategory {category name}`. Replace the `{category name}` with the name of the category. Obviously, ensure you have created the category beforehand. An example usage is `/changesetting ticketsCategory orders`.

Setting up the company name is purely optional and doesn't affect anything other than the message sent by the bot upon creation of a ticket. This is the default message sent to the user upon creation of the ticket.
> Greetings, arendameth! Thank you for choosing us! 
I will be your personal assistant during this ticket. How may I be of help to you today?

You can change this by using `/changesetting companyName {name}`. For example, using `/changesetting companyName Hernandez Corporation` will change the message to:
> Greetings, arendameth! Thank you for choosing Hernandez Corporation! 
I will be your personal assistant during this ticket. How may I be of help to you today?

### 5- Setting up permissions
By default, all bot commands can be used only by those who have administrative permissions, except the `/prices` command, which can be used by everyone. In order to configure what commands can be used by who, you can go to **Server Settings -> Integrations -> S.A.L.A.**, then edit the permissions as you please.

Additionally, certain permissions within the bot script must be set up. You can do this using `/addperm {permission type} {role}`. Accepted strings into the parameter `permission type` are explained below.
| Permission Type | Information |
| --------------- | ----------- |
| closeTickets    | The roles which have permissions to close tickets. By default, everyone who has access to the ticket will be able to close it. Changing this setting will restrict closing the ticket to those roles only. Do note that no matter what this setting is, server administrators and ticket creator will **always** have the permission to close the ticket. |
| ticketStaff     | The roles which are given access to tickets upon the ticket creation. You do not need to give truckers this permission, as they already get permission to the ticket when they claim it. |
| deliveryRolesTag | While not technically a permission, this setting controls which roles the bot will tag to claim a new order in the assigned `receiptsChannel`, when the order's receipt is printed. |

You can also remove permissions using `/removeperm {permission type} {role}`, or clear the permissions using `/clearperm {permission_type} {role}`.

### 6- Setting up prices
You need to set up the prices you are charging for your deliveries using `/setprice {price type} {new value}`. You can also use the same command for setting up a discount. The following table explains the accepted parameters.
| Price Type | Information |
| --------------- | ----------- |
| business    | The price per one business crate. |
| fuel     | The price per one fuel liter. |
| fabrics | The price per one fabrics crate. |
| metals | The price per one metals crate. |
| discount | A discount you may or not offer. This is optional to set up at any time and is defaulted to 0. The value can't be less than 0 or more than 100. The discount is applied globally to all of your prices. In order to discount a single item's price, you need to manually set its price. |

At this point, you have fully set up the bot and its ready to be used within your server.

## Using the bot
### As a company manager
When new clients create orders, you are expected to create a receipt which is sent to to the previously set `receiptsChannel` for employees to claim and carry out. You can do this using `/receipt {client name} {delivery type} {crates_or_fuel} {location} {price}`
- **Client name** is self explanatory
- **Delivery type** is the type of delivery. You'll be given a list of choices to pick from for this parameter. They're also listed below in the table
- **Crates or fuel** is the amount of crates or fuel being delivered. This field accepts strings so that it can be broken down in case of multiple deliveries.
- **Location** is the GPS location that the trucker is expected to deliver to.
- **Price** is self explanatory.

| Delivery Type |
| ------------- |
| Warehouse - Fabrics |
| Warehouse - Metals |
| Business - Hardware Crates (Toolstores) |
| Business - Weapons Crates (Ammunations ) |
| Food Crates (Restuarants and Bars) |
| Pharmaceutical Crates (Pharmacies) |
| Electronic Crates (24/7s) |
| Vehicle Parts Crates (PNS) |
| Agriculture Crates (Seed Stores) |
| Fuel (Gas Stations) |
| Multiple Deliveries |

For convenience, entering a wrong number will display this list. Upon using the command, a receipt will be generated and sent to the `receiptsChannel`. This receipt will be available for any trucker to claim. Once claimed, the ability to claim it further will be closed, and the claiming trucker will be granted access to the order ticket.

### As an employee
There's nothing for you to do as an employee in a company using this bot. You simply click **Claim** when you're tagged for a new order and carry out the order.
