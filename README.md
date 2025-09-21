# 📋 Task Manage - Flutter Приложение

![Flutter](https://img.shields.io/badge/Flutter-3.0+-blue.svg)
![Dart](https://img.shields.io/badge/Dart-2.19+-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)
![Platform](https://img.shields.io/badge/Platform-Android%20|%20iOS%20|%20Web%20|%20Windows-lightgrey.svg)

<div align="center">
  <img src="https://img.icons8.com/color/96/000000/task.png" alt="Task Manager Icon"/>
  <h3>Элегантное приложение для управления задачами с полным набором CRUD операций</h3>
</div>

## ✨ Возможности

- ✅ **Добавление задач** - Быстрый ввод новых задач через TextField
- ✏️ **Редактирование задач** - Изменение существующих задач с мгновенным обновлением
- 🗑️ **Удаление задач** - Свайп-жесты или кнопка удаления
- ☑️ **Отметка выполнения** - Чекбоксы для отметки выполненных задач
- 🎨 **Material Design** - Современный красивый интерфейс
- 📱 **Полная адаптивность** - Работает на Android, iOS, Web и Windows
- ⚡ **Горячая перезагрузка** - Мгновенное обновление при разработке

## 🚀 Технологии

- **Flutter 3.0+** - Современный кроссплатформенный фреймворк
- **Dart 2.19+** - Статически типизированный язык программирования
- **Material Design 3** - Последняя версия дизайн-системы Google
- **StatefulWidget** - Эффективное управление состоянием приложения
- **ListView.builder** - Оптимизированное отображение списков
- **TextField** - Поле ввода с валидацией
- **Dismissible** - Поддержка свайп-жестов


## 🛠️ Установка и запуск

### Предварительные требования

- Flutter SDK 3.0 или выше
- Dart SDK 2.19 или выше
- Устройство или эмулятор (Android/iOS)
- Браузер (для web-версии)

### Клонирование репозитория

```bash
git clone https://github.com/panfiloow/task_manager.git
cd task_manager
```
Установка зависимостей
```bash
flutter pub get
```
Запуск приложения
```bash
# Для Android (эмулятор или устройство)
flutter run -d android

# Для iOS (требуется Mac)
flutter run -d ios

# Для Web (Chrome)
flutter run -d chrome

# Для Windows
flutter run -d windows

# Для автоматического выбора устройства
flutter run
```

## 📖 Как пользоваться приложением

### ➕ Добавление новой задачи
1. **Найдите текстовое поле** в верхней части экрана
2. **Введите текст** вашей задачи
3. **Нажмите кнопку** ➕ или клавишу **Enter** на клавиатуре
4. **Задача автоматически появится** в списке ниже

### ✏️ Редактирование существующей задачи
- **Способ 1:** Нажмите на иконку **карандаша** ✏️ рядом с нужной задачей
- **Способ 2:** **Свайпните задачу вправо** для быстрого редактирования
- **Измените текст** в появившемся поле ввода
- **Сохраните изменения** кнопкой 💾 или клавишей Enter

### 🗑️ Удаление задачи
- **Способ 1:** Нажмите на иконку **корзины** 🗑️ рядом с задачей
- **Способ 2:** **Свайпните задачу влево** для быстрого удаления
- **Способ 3:** Выполните **долгое нажатие** на задачу и подтвердите удаление

## 🔧 Ключевые компоненты кода

### StatefulWidget с управлением состоянием
```dart
class TaskManagerScreen extends StatefulWidget {
  @override
  _TaskManagerScreenState createState() => _TaskManagerScreenState();
}
```
Эффективный ListView.builder для отображения задач
```dart
ListView.builder(
  itemCount: _tasks.length,
  itemBuilder: (context, index) {
    return Dismissible(
      key: Key(_tasks[index].id.toString()),
      child: TaskItem(_tasks[index]),
    );
  },
)
```
TextField с контроллером для ввода задач
```dart
TextField(
  controller: _taskController,
  decoration: InputDecoration(
    labelText: 'Введите задачу',
    border: OutlineInputBorder(),
    hintText: 'Что нужно сделать?',
  ),
  onSubmitted: (_) => _addTask(),
)
```
Полный набор CRUD операций
Create - Создание новых задач
```dart
void _addTask() {
  final String taskText = _taskController.text.trim();
  if (taskText.isEmpty) return;
  
  setState(() {
    _tasks.add(Task(
      id: _nextId++,
      title: taskText,
      createdAt: DateTime.now(),
    ));
    _taskController.clear();
  });
}
```
Read - Отображение списка задач
```dart
ListView.builder(
  itemCount: _tasks.length,
  itemBuilder: (context, index) {
    final task = _tasks[index];
    return ListTile(
      title: Text(task.title),
      subtitle: Text('Создано: ${_formatDate(task.createdAt)}'),
    );
  },
)
```
Update - Редактирование задач
```dart
void _editTask(Task task) {
  setState(() {
    _editingTask = task;
    _taskController.text = task.title;
  });
}
```
Delete - Удаление задач
```dart
void _deleteTask(int id) {
  setState(() {
    _tasks.removeWhere((task) => task.id == id);
  });
}
```
Dismissible для свайп-жестов
```dart
Dismissible(
  key: Key(task.id.toString()),
  background: Container(color: Colors.red),
  secondaryBackground: Container(color: Colors.blue),
  onDismissed: (direction) {
    if (direction == DismissDirection.startToEnd) {
      _deleteTask(task.id!);
    }
  },
  child: ListTile(...),
)
```
Модель данных Task
```dart
class Task {
  int? id;
  String title;
  bool isCompleted;
  DateTime createdAt;

  Task({
    this.id,
    required this.title,
    this.isCompleted = false,
    required this.createdAt,
  });
}
```

## 📝 Лицензия

### MIT License

Copyright (c) 2024 Панфилов Илья

Данная лицензия разрешает лицам, получившим копию данного программного обеспечения и сопутствующей документации (в дальнейшем «Программное обеспечение»), безвозмездно использовать Программное обеспечение без ограничений, включая неограниченное право на использование, копирование, изменение, слияние, публикацию, распространение, сублицензирование и/или продажу копий Программного обеспечения, а также лицам, которым предоставляется данное Программное обеспечение, при соблюдении следующих условий:

Указанное выше уведомление об авторском праве и данные условия должны быть включены во все копии или значительные части Программного обеспечения.

ПРОГРАММНОЕ ОБЕСПЕЧЕНИЕ ПРЕДОСТАВЛЯЕТСЯ «КАК ЕСТЬ», БЕЗ КАКИХ-ЛИБО ГАРАНТИЙ, ЯВНО ВЫРАЖЕННЫХ ИЛИ ПОДРАЗУМЕВАЕМЫХ, ВКЛЮЧАЯ, НО НЕ ОГРАНИЧИВАЯСЬ ГАРАНТИЯМИ ТОВАРНОЙ ПРИГОДНОСТИ, СООТВЕТСТВИЯ ПО КОНКРЕТНОМУ НАЗНАЧЕНИЮ И НЕНАРУШЕНИЯ ПРАВ. НИ В КАКОМ СЛУЧАЕ АВТОРЫ ИЛИ ПРАВООБЛАДАТЕЛИ НЕ НЕСУТ ОТВЕТСТВЕННОСТИ ПО ИСКАМ О ВОЗМЕЩЕНИИ УЩЕРБА, УБЫТКОВ ИЛИ ДРУГИХ ТРЕБОВАНИЙ ПО ДЕЙСТВУЮЩЕМУ ПРАВУ, ДОГОВОРУ ИЛИ ИНОМУ, ВОЗНИКШИМ ИЗ, ИМЕЮЩИМ ПРИЧИНОЙ ИЛИ СВЯЗАННЫМ С ПРОГРАММНЫМ ОБЕСПЕЧЕНИЕМ ИЛИ ИСПОЛЬЗОВАНИЕМ ПРОГРАММНОГО ОБЕСПЕЧЕНИЯ ИЛИ ИНЫМИ ДЕЙСТВИЯМИ С ПРОГРАММНЫМ ОБЕСПЕЧЕНИЕМ.
