# parking-system
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
public class SmartParkingSystem extends Frame 
implements ActionListener {
 
 // Declare GUI components
 private TextField vehicleNumberField;
 private Button checkAvailabilityButton, paymentButton, 
reserveButton, confirmButton;
 private Label statusLabel;
 private boolean spotAvailable = false; // Flag for 
availability of the spot
 private boolean paymentMade = false; // Flag to check if 
payment was made
 
 // Constructor to set up the GUI
 public SmartParkingSystem() {
 // Frame Setup
 setTitle("Smart Parking System");
 setSize(400, 300);
 setLayout(new BorderLayout());
 
 // Create a panel for components in vertical alignment
 Panel inputPanel = new Panel();
 inputPanel.setLayout(new BoxLayout(inputPanel, 
BoxLayout.Y_AXIS)); // Use Y_AXIS for vertical layout
 
 // Create and add components to the panel
 Label vehicleNumberLabel = new Label("Enter 
Vehicle Number:");
 vehicleNumberField = new TextField(20);
 
 checkAvailabilityButton = new Button("Check 
Availability");
 paymentButton = new Button("Make Payment");
 reserveButton = new Button("Reserve Spot");
 confirmButton = new Button("Confirm Spot");
 
 statusLabel = new Label("Status: ");
 
 // Add components to the panel (one per line)
 inputPanel.add(vehicleNumberLabel);
 inputPanel.add(vehicleNumberField);
 inputPanel.add(checkAvailabilityButton);
 inputPanel.add(paymentButton);
 inputPanel.add(reserveButton);
 inputPanel.add(confirmButton);
 inputPanel.add(statusLabel);
 
 // Add input panel to the center of the frame
 add(inputPanel, BorderLayout.CENTER);
 
 // Add action listeners to buttons
 checkAvailabilityButton.addActionListener(this);
 paymentButton.addActionListener(this);
 reserveButton.addActionListener(this);
 confirmButton.addActionListener(this);
 
 // Initially, disable all buttons except for Check 
Availability
 paymentButton.setEnabled(false);
 reserveButton.setEnabled(false);
 confirmButton.setEnabled(false);
 
 // Close the window on close button click
 addWindowListener(new WindowAdapter() {
 public void windowClosing(WindowEvent we) {
 System.exit(0);
 }
 });
 }
 
 // Implement ActionListener's actionPerformed method
 @Override
 public void actionPerformed(ActionEvent e) {
 // Check availability button clicked
 
if (e.getSource() == checkAvailabilityButton) {
 
 String vehicleNumber = 
vehicleNumberField.getText();
 if (!vehicleNumber.isEmpty()) {
 // Simulating checking availability (just a random 
decision here)
 spotAvailable = Math.random() > 0.5;
 
 if (spotAvailable) {
 statusLabel.setText("Status: Spot Available for 
Vehicle " + vehicleNumber);
 paymentButton.setEnabled(true); // Enable 
payment button
 } else {
 statusLabel.setText("Status: No Available 
Spot");
 paymentButton.setEnabled(false); // Disable 
further actions
 reserveButton.setEnabled(false);
 confirmButton.setEnabled(false);
 }
 } else {
 statusLabel.setText("Status: Please enter a vehicle 
number.");
 }
 }
 // Payment button clicked
 if (e.getSource() == paymentButton) {
 // Simulate payment processing
 paymentMade = true;
 statusLabel.setText("Status: Payment Successful.");
 reserveButton.setEnabled(true); // Enable reserve 
button
 }
 
 // Reserve spot button clicked
 if (e.getSource() == reserveButton) {
 if (paymentMade) {
 statusLabel.setText("Status: Spot Reserved.");
 confirmButton.setEnabled(true); // Enable 
confirm button
 } else {
 statusLabel.setText("Status: Payment Required 
Before Reserving.");
 }
 }
 
 // Confirm spot button clicked
 if (e.getSource() == confirmButton) {
 statusLabel.setText("Status: Parking Spot 
Confirmed.");
 resetSystem(); // Reset system for the next user
 }
 
}
// Method to reset the system for a new user
 private void resetSystem() {
 vehicleNumberField.setText("");
 paymentMade = false;
 spotAvailable = false;
 statusLabel.setText("Status: ");
 paymentButton.setEnabled(false);
 reserveButton.setEnabled(false);
 confirmButton.setEnabled(false);
 }
 
 // Main method to run the system
 public static void main(String[] args) {
 SmartParkingSystem parkingSystem = new 
SmartParkingSystem();
 parkingSystem.setVisible(true);
 }
}
