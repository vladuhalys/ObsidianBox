Link to: **[[Asynchronous programming]]**

> [!INFO]
> Stream у Dart — це асинхронна послідовність подій або даних. Вони дозволяють виконувати обробку даних, коли вони стають доступними, не блокуючи основний потік виконання. Це дуже корисно для роботи з подіями, запитами HTTP, потоковими даними та іншими асинхронними операціями.

# Основні моменти про Stream:

### Два типи стрімів:
- **Одноразовий ([[Single subscription]])**: Підписник може підписатися тільки один раз на стрім.
- **Широкомовний ([[Broadcast]])**: На стрім може підписатися багато підписників, і всі вони отримують події одночасно.

### Основні методи:
- `listen()`: підписується на стрім і дозволяє обробляти події.
- `await for`: використовується для асинхронного перебору подій стріму.
- `where()`, `map()`, `take()`, `skip()`: оператори для фільтрації, трансформації та вибірки даних зі стріму.

### Створення Stream:
- **StreamController**: використовується для створення та контролю стріму.

```dart
var controller = StreamController<int>();
controller.add(1); // Додає подію в стрім
controller.stream.listen((data) {
  print(data); // Обробляє події
});
```

### Асинхронні операції зі стрімами:

Використовуючи ключове слово `await`, можна зручно працювати з потоками даних, не блокуючи основний потік.

```dart
await for (var event in stream) {
  print(event);
}
```

---
## Приклади використання:


### Читання з файлу асинхронно:

```dart
import 'dart:io';

void main() async {
  var file = File('example.txt');
  Stream<List<int>> inputStream = file.openRead();

  await for (var chunk in inputStream) {
    print(chunk);  // Обробка потоку даних з файлу
  }
}
```

### Реалізація стріму для лічильника:

```dart
Stream<int> countStream(int max) async* {
  for (int i = 0; i <= max; i++) {
    yield i;  // Передача значень у стрім
    await Future.delayed(Duration(seconds: 1));  // Імітація затримки
  }
}
```
