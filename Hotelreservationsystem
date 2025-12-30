import java.io.*;
import java.util.*;

class Room {
    int roomNumber;
    String category;
    double price;
    boolean isBooked;

    Room(int roomNumber, String category, double price) {
        this.roomNumber = roomNumber;
        this.category = category;
        this.price = price;
        this.isBooked = false;
    }
}

class Booking {
    String customerName;
    int roomNumber;
    String category;
    double amountPaid;

    Booking(String customerName, int roomNumber, String category, double amountPaid) {
        this.customerName = customerName;
        this.roomNumber = roomNumber;
        this.category = category;
        this.amountPaid = amountPaid;
    }
}

public class HotelReservationSystem {

    static ArrayList<Room> rooms = new ArrayList<>();
    static Scanner sc = new Scanner(System.in);
    static final String FILE_NAME = "bookings.txt";

    public static void main(String[] args) {
        initializeRooms();

        while (true) {
            System.out.println("\n===== HOTEL RESERVATION SYSTEM =====");
            System.out.println("1. View Available Rooms");
            System.out.println("2. Book a Room");
            System.out.println("3. Cancel Reservation");
            System.out.println("4. View Bookings");
            System.out.println("5. Exit");
            System.out.print("Enter choice: ");

            int choice = sc.nextInt();
            sc.nextLine();

            switch (choice) {
                case 1 -> viewRooms();
                case 2 -> bookRoom();
                case 3 -> cancelBooking();
                case 4 -> viewBookings();
                case 5 -> {
                    System.out.println("Thank you for using the system!");
                    System.exit(0);
                }
                default -> System.out.println("Invalid choice!");
            }
        }
    }

    static void initializeRooms() {
        rooms.add(new Room(101, "Standard", 1500));
        rooms.add(new Room(102, "Standard", 1500));
        rooms.add(new Room(201, "Deluxe", 2500));
        rooms.add(new Room(202, "Deluxe", 2500));
        rooms.add(new Room(301, "Suite", 4000));
    }

    static void viewRooms() {
        System.out.println("\nAvailable Rooms:");
        for (Room room : rooms) {
            if (!room.isBooked) {
                System.out.println("Room " + room.roomNumber + " | " + room.category + " | ₹" + room.price);
            }
        }
    }

    static void bookRoom() {
        System.out.print("Enter your name: ");
        String name = sc.nextLine();

        viewRooms();
        System.out.print("Enter room number to book: ");
        int roomNo = sc.nextInt();

        for (Room room : rooms) {
            if (room.roomNumber == roomNo && !room.isBooked) {
                room.isBooked = true;

                System.out.println("Processing payment of ₹" + room.price + "...");
                System.out.println("Payment Successful!");

                Booking booking = new Booking(name, room.roomNumber, room.category, room.price);
                saveBooking(booking);

                System.out.println("Room booked successfully!");
                return;
            }
        }
        System.out.println("Room not available!");
    }

    static void cancelBooking() {
        System.out.print("Enter room number to cancel booking: ");
        int roomNo = sc.nextInt();

        for (Room room : rooms) {
            if (room.roomNumber == roomNo && room.isBooked) {
                room.isBooked = false;
                removeBooking(roomNo);
                System.out.println("Booking cancelled successfully!");
                return;
            }
        }
        System.out.println("No booking found for this room!");
    }

    static void saveBooking(Booking booking) {
        try (FileWriter fw = new FileWriter(FILE_NAME, true)) {
            fw.write(booking.customerName + "," +
                    booking.roomNumber + "," +
                    booking.category + "," +
                    booking.amountPaid + "\n");
        } catch (IOException e) {
            System.out.println("Error saving booking!");
        }
    }

    static void viewBookings() {
        System.out.println("\nBooking Details:");
        try (BufferedReader br = new BufferedReader(new FileReader(FILE_NAME))) {
            String line;
            while ((line = br.readLine()) != null) {
                String[] data = line.split(",");
                System.out.println("Name: " + data[0] +
                        " | Room: " + data[1] +
                        " | Category: " + data[2] +
                        " | Paid: ₹" + data[3]);
            }
        } catch (IOException e) {
            System.out.println("No bookings found!");
        }
    }

    static void removeBooking(int roomNo) {
        File inputFile = new File(FILE_NAME);
        File tempFile = new File("temp.txt");

        try (BufferedReader br = new BufferedReader(new FileReader(inputFile));
             FileWriter fw = new FileWriter(tempFile)) {

            String line;
            while ((line = br.readLine()) != null) {
                if (!line.contains("," + roomNo + ",")) {
                    fw.write(line + "\n");
                }
            }
        } catch (IOException e) {
            System.out.println("Error updating bookings!");
        }

        inputFile.delete();
        tempFile.renameTo(inputFile);
    }
}
