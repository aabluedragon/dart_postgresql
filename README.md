# NOTIFY support for the Dart PostgreSQL database driver

## Usage Example:
```dart
main(List<String> args) async {
  var uri = 'postgres://user:pass@localhost:5432/yourdbname';
  var conn = await connect(uri);
  await conn.execute("LISTEN something;");

  new Timer.periodic(const Duration(milliseconds: 500), (t) async {
    var notifications = await conn.getNotifications();
    for(var item in notifications) {
      print('Notification received: ${item.pid} ${item.condition} ${item.text}');
    }
  });
}
```
