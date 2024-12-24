# Movie Ticket Booking Application

## Understand Requirements

We need to create a movie ticket booking application. 

- **Theatre**: Contains multiple Screens that run Shows for different Movies.
- **Show**: Each Show has:
  - A particular Movie
  - Start time
  - Duration
  - A specific Screen in the theatre
- **Screen**: Each Screen has an arrangement of Seats that can be booked by Users.
Assume all Users are registered, authenticated, and logged in to the Application.
1. **UserBookingSession**: 
   - Once a User selects a particular show to book tickets for, a UserBookingSession starts.
   - Within this session, a User can:
     - Get the Available Seats for the show.
     - Select the Seats they wish to book.
   - It is a ‘good to have’ feature for the Application to limit the number of seats a User can book in a Ticket.

2. **Seat Availability**:
   - Once the user has selected a group of seats, these seats should become **TEMPORARILY_UNAVAILABLE** to all other Users.

3. **Payment Process**:
   - The User then proceeds to make payment, which can either be **SUCCESS** or **FAILURE**.
   - If Payment **FAILED**:
     - The user can retry Payment for a maximum number of times.
     - Beyond maximum retries, the seats are made **AVAILABLE**.
   - If Payment **SUCCEEDS**:
     - A Ticket or Booking Confirmation is generated and made available to the User.
     - The UserBookingSession is closed, and the Seats are made **PERMANENTLY_UNAVAILABLE**.
4. **Session Closure**:
   - A User can also explicitly close the UserBookingSession after selecting seats and before making payment. 
   - In this case, the seats selected are made **AVAILABLE** once again.


## Identify Classes, Objects, and Relationships

### Theatre

- **Theatre** has multiple **Screens**.

```
  class Theatre {
    id: string;
    name: string;
    screens: Screen[];

    constructor(id: string, name: string, screens: Screen[]) {
      this.id = id;
      this.name = name;
      this.screens = screens;
    }
  }
```

### Movie

- **Movie** has a **Id**.
- **Movie** has a **Name**.
- **Movie** has a **Duration**.
- **Movie** has a **Language**.
- **Movie** has a **Genre**.
- **Movie** has a **Release Date**.

```

  enum Language {
    HINDI,
    ENGLISH,
    MARATHI,
    TELUGU,
    TAMIL,
    KANNADA,
    BENGALI
  }

  enum Genre {
    ACTION,
    ADVENTURE,
    COMEDY,
    DRAMA,
    FANTASY,
    HORROR,
    MYSTERY,
    ROMANCE,
    SCIENCE_FICTION,
  }

  class Movie {
    id: string;
    name: string;
    duration: number;
    language: Language;
    genre: Genre;
    releaseDate: Date;
  }
```

### Screen

- **Screen** has multiple **Seats**.
- **Screen** has a **Screen Number**.

```
  class Screen {
    id: string;
    screenNumber: number;
    seats: Seat[];
  }
```

### Show

- **Show** has a **Id**.
- **Show** has a **Movie**.
- **Show** has a **Start Time**.
- **Show** has a **Duration**.
- **Show** has a **Screen**.

```
  class Show {
    id: string;
    movie: Movie;
    startTime: Date;
    duration: number;
    screen: Screen;
  }
```

### Seat

- **Seat** has a **Id**.
- **Seat** has a **Row**.
- **Seat** has a **Column**.
- **Seat** has a **Price**.
- **Seat** has a **Seat Number**.
- **Seat** has a **Status**.
- **Seat** has a **Seat Type**.

```
  enum SeatStatus {
    AVAILABLE,
    TEMPORARILY_UNAVAILABLE,
    PERMANENTLY_UNAVAILABLE
  }

  enum SeatType {
    REGULAR,
    PREMIUM
  }

  class Seat {
    id: string;
    row: number;
    column: number;
    price: number;
    seatNumber: string;
    status: SeatStatus;
    seatType: SeatType;
  }
```

### Booking

- **Booking** has a **Id**.
- **Booking** has a **Show**.
- **Booking** has a **Seats**.
- **Booking** has a **Payment**.
- **Booking** has a **Status**.
- **Booking** has a **UserId**.

```
  enum BookingStatus {
    PENDING,
    CONFIRMED,
    CANCELLED
  }

  class Booking {
    id: string;
    show: Show;
    seats: Seat[];
    payment: Payment;
    status: BookingStatus;
    userId: string;
  }
``` 

### Payment

- **Payment** has a **Id**.
- **Payment** has a **Amount**.
- **Payment** has a **Status**.
- **Payment** has a **BookingId**.

```
  enum PaymentStatus {
    SUCCESS,
    FAILURE
  }

  class Payment {
    id: string;
    amount: number;
    status: PaymentStatus;
    bookingId: string;
  }
``` 

### User

- **User** has a **Id**.
- **User** has a **Name**.
- **User** has a **Email**.

```
  class User {
    id: string;
    name: string;
    email: string;
  }
```

## Define Methods






## Data Structures
Using list data structure, we can store the following:

- List of all the movies in the theatre.
- List of all the shows in the theatre.
- List of all the bookings in the theatre.
- List of all the payments in the theatre.
- List of all the users in the theatre.

```
   List<Movie> movies;
   List<Show> shows;
   List<Booking> bookings;
   List<Payment> payments;
   List<User> users;
```

## State Diagrams And Sequence Diagrams
... coming soon

## Error Handling

Throwing error when the seat is not found in the screen or the show is not found in the theatre.


## Design Patterns

- **Factory Pattern**: To create the objects of the classes.
- **Singleton Pattern**: To ensure that there is only one instance of the class.
- **Observer Pattern**: To notify the users when the seats are available.
- **Command Pattern**: To execute the commands for the user.
- **State Pattern**: To change the state of the seat when the user books the seat.
- **Strategy Pattern**: To change the strategy of the payment when the user makes the payment.



