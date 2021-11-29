


``` java

public class CarRental {

  public void book(LocalDate start, LocalDate end) {
    System.out.println("Booking car for " + start + " to " + end);
  }

}


public class Hotel {

  public void book(LocalDate checkinDate, LocalDate checkoutDate) {
    System.out.println("Booking hotel for " + checkinDate + " to " + checkoutDate);
  }

}

public class Flight {

  public void bookOutwardJourney(LocalDate start) {
    System.out.println("Outbound flight booked for " + start);
  }

  public void bookReturnJourney(LocalDate end) {
    System.out.println("Return flight booked for " + end);
  }


}


public class VacationFacade {

  public void book(LocalDate startDate, LocalDate endDate) {
    Flight flight = new Flight();
    flight.bookOutwardJourney(startDate);
    flight.bookReturnJourney(endDate);

    Hotel hotel = new Hotel();
    hotel.book(startDate, endDate);

    CarRental carRental = new CarRental();
    carRental.book(startDate, endDate);
  }

}


// client doesn't have to know the detail

public class VacationPackage {

  public static void main(String[] args) {
    LocalDate startDate = LocalDate.of(2021, 8, 1);
    LocalDate endDate = LocalDate.of(2021, 8, 15);

    VacationFacade vacationFacade = new VacationFacade();
    vacationFacade.book(startDate, endDate);

  }

}


```