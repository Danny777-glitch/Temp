# 💻 Flutter Exam — CODE for ALL Part A (2-Mark) Questions

*Write the code first in the exam, then 1-2 lines explaining it. That's enough for full 2 marks.*

---

### 1. Widget lifecycle events in a healthcare app (patient records)

```dart
class PatientScreen extends StatefulWidget {
  @override
  State<PatientScreen> createState() => _PatientScreenState();
}
class _PatientScreenState extends State<PatientScreen> {
  @override
  void initState() {
    super.initState();
    loadPatientRecords();   // called once when screen opens
  }
  void loadPatientRecords() {
    setState(() {
      // update patient data here
    });
  }
  @override
  void dispose() {
    // release resources (close streams, cancel timers)
    super.dispose();
  }
  @override
  Widget build(BuildContext context) => Text("Patient Records");
}
```

---

### 2. Layout adaptation during orientation changes

```dart
OrientationBuilder(
  builder: (context, orientation) {
    return orientation == Orientation.portrait
        ? Column(children: [Text("Stacked layout")])
        : Row(children: [Text("Side-by-side layout")]);
  },
)
```

---

### 3. Widget Tree & Element Tree (movie ticket booking – seat selection)

```dart
class SeatSelector extends StatefulWidget {
  @override
  State<SeatSelector> createState() => _SeatSelectorState();
}
class _SeatSelectorState extends State<SeatSelector> {
  String? selectedSeat;
  @override
  Widget build(BuildContext context) {
    // Widget tree (blueprint) rebuilt here.
    // Element tree keeps state (selectedSeat) and reuses
    // unchanged elements, only updating the changed seat.
    return Row(children: [
      GestureDetector(
        onTap: () => setState(() => selectedSeat = "A1"),
        child: Text(selectedSeat == "A1" ? "Selected" : "A1"),
      ),
    ]);
  }
}
```

---

### 4. Widget architecture for travel booking app (orientation + animation)

```dart
class BookingFlow extends StatefulWidget {
  @override
  State<BookingFlow> createState() => _BookingFlowState();
}
class _BookingFlowState extends State<BookingFlow> {
  bool confirmed = false;
  @override
  Widget build(BuildContext context) {
    return OrientationBuilder(
      builder: (context, orientation) {
        return AnimatedContainer(
          duration: Duration(milliseconds: 500),
          color: confirmed ? Colors.green : Colors.grey,
          child: orientation == Orientation.portrait
              ? Column(children: [Text("Search"), Text("Details"), Text("Confirm")])
              : Row(children: [Text("Search"), Text("Details"), Text("Confirm")]),
        );
      },
    );
  }
}
```

---

### 5. Widget structure for student registration form + validation

```dart
final _formKey = GlobalKey<FormState>();

Form(
  key: _formKey,
  child: Column(children: [
    TextFormField(
      decoration: InputDecoration(labelText: "Name"),
      validator: (v) => (v == null || v.isEmpty) ? "Name required" : null,
    ),
    TextFormField(
      decoration: InputDecoration(labelText: "Roll No"),
      validator: (v) => (v == null || v.isEmpty) ? "Roll No required" : null,
    ),
    ElevatedButton(
      onPressed: () {
        if (_formKey.currentState!.validate()) {
          // submit form
        }
      },
      child: Text("Submit"),
    ),
  ]),
)
```

---

### 6. Widget layout for restaurant app (menu categories + items)

```dart
Column(children: [
  SizedBox(
    height: 40,
    child: Row(children: [
      Chip(label: Text("Starters")),
      Chip(label: Text("Main Course")),
      Chip(label: Text("Desserts")),
    ]),
  ),
  Expanded(
    child: ListView(children: [
      Card(child: ListTile(title: Text("Pizza"), subtitle: Text("₹250"))),
      Card(child: ListTile(title: Text("Pasta"), subtitle: Text("₹200"))),
    ]),
  ),
])
```

---

### 7. Reusable Dart class for customer feedback (service app)

```dart
class Feedback {
  String customerName;
  String comment;
  int rating;

  Feedback(this.customerName, this.comment, this.rating);

  void display() {
    print("$customerName rated $rating stars: $comment");
  }
}

void main() {
  var f1 = Feedback("Aathi", "Great service", 5);
  var f2 = Feedback("Ravi", "Could be faster", 3);
  f1.display();
  f2.display();
}
```

---

### 8. Compare initState() and dispose()

```dart
class DemoScreen extends StatefulWidget {
  @override
  State<DemoScreen> createState() => _DemoScreenState();
}
class _DemoScreenState extends State<DemoScreen> {
  @override
  void initState() {
    super.initState();
    print("initState: runs ONCE when widget is created — start data fetch here");
  }
  @override
  void dispose() {
    print("dispose: runs ONCE when widget is removed — cancel timers/controllers here");
    super.dispose();
  }
  @override
  Widget build(BuildContext context) => Text("Demo");
}
```

---

### 9. UI using Container for a login screen

```dart
Container(
  padding: EdgeInsets.all(20),
  decoration: BoxDecoration(
    color: Colors.white,
    borderRadius: BorderRadius.circular(10),
  ),
  child: Column(children: [
    TextField(decoration: InputDecoration(labelText: "Username")),
    TextField(decoration: InputDecoration(labelText: "Password"), obscureText: true),
    ElevatedButton(onPressed: () {}, child: Text("Login")),
  ]),
)
```

---

### 10. Dart function — total bill for food delivery app

```dart
double calculateTotal(List<double> prices) {
  double total = 0;
  for (var price in prices) {
    total += price;
  }
  return total;
}

void main() {
  List<double> cart = [120.0, 80.0, 45.5];
  print("Total bill: ₹${calculateTotal(cart)}");
}
```

---

### 11. Dart class — customer details in online shopping app

```dart
class Customer {
  String name;
  String address;
  String phone;

  Customer(this.name, this.address, this.phone);

  void showDetails() {
    print("Name: $name, Address: $address, Phone: $phone");
  }
}

void main() {
  var customer = Customer("Aathi", "Coimbatore", "9876543210");
  customer.showDetails();
}
```

---

### 12. Dart functions & packages in a weather forecasting app

```dart
import 'package:http/http.dart' as http;   // package for API calls
import 'dart:convert';

double celsiusToFahrenheit(double celsius) {
  return (celsius * 9 / 5) + 32;           // reusable Dart function
}

Future<void> fetchWeather() async {
  final response = await http.get(Uri.parse("https://api.weather.com/data"));
  var data = jsonDecode(response.body);
  print("Temp in F: ${celsiusToFahrenheit(data['tempC'])}");
}
```

---

## ✅ Quick Reminder
For each answer in the exam: **write the code block above → then add 1 line explaining what it does.** That alone secures full marks for 2-mark questions — no need to write long theory.
