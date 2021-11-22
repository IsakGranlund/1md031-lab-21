## 04 JavaScript and Vue

- [x] You have a menu.json file which contains at least three different burgers with respective attributes

Your Home.vue file:
- [x] ... contains a MenuItem constructor (that is not used)
- [x] ... loads the information from the menu.json object and inserts the information to the burger selection section
- [x] ... allows the customer to click in the interactive map to select delivery location
- [x] ... has an order button that sends the information from the text boxes, the gender, all items on the order, and the delivery location to the server (to be realyed to the dispatcher)

Your Burger.vue component:
- [x] ... allows adding and removing burgers from the order
- [x] ... only displays allergy information if relevant (either only if it contains gluten or lactose, or only if it's gluten or lactose free)

Your Dispatcher.vue file:
- [x] ... shows for every order :
    - [x] a location on the map
    - [x] the order information
    - [x] the customer information

## Optional
- [ ] Only allow the order to be sent if all necessary information are provided
- [ ] Display receipt on the customer page as well
- [ ] Allow the dispatcher to handle orders by providing buttons next to every order that can switch the order status to "in preparation" and "done"
- [ ] Display the order status to the customer and update it in the customer view if updated by the dispatcher
- [ ] Show the order status for the customer as well.
- [ ] Find a better visualization for what orders belong to which location on the map
