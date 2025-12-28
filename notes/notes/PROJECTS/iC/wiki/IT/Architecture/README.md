# Architecture

System consists of multiple more or less independent entities which communicates with each other. Purpose of architecture folder is to provide complete view.

To see full architecture picture, see `icsystems-current.svg` or `icsystems-current.png`

Picture is created using web application [draw.io](https://draw.io). Source code is enclosed as `icsystems-current.drawio`

## Components

### Sensor

HW part installed on customer site consisting from a Raspberry Pi and a camera.

##### Responsibilities

- filming required area
- processing frames with ultimate goal detect and track humans
- sending events for required behave of  humans

##### Technological Stack

- Python
- Rust (icclient)
- ?? TODO Filip and/or Erik: what else


### Cloud

Web application providing processed events to customer same as serving to our sales representatives for setting up a customer and its users.

##### Responsibilities

- persisting events
- events aggregation
- report creation
- report sending via email
- providing visualisation to customers

##### Technological Stack

- front-end: JavaScript (VueJS, jQuery)
- back-end: PHP, Java
- database: PostgreSQL 

### Monitoring

Web application providing monitoring of installed sensors same as serving to our technical support for setting up the sensors.

##### Responsibilities

- heal-check of sensors
- remote control of sensors
- proxy for Cloud to get screenshots from sensors

##### Technological Stack

- front-end: JavaScript (React)
- back-end: Rust
- database: TimescaleDB

### API

REST API serving to customers application for fetching reports based on received events from sensors.

##### Responsibilities

- providing REST API for fetching reports (?? TODO Pavel Merta: or events)


##### Technological Stack

- back-end: PHP, Java
- database: PostgreSQL