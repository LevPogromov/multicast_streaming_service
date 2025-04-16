# Multicast Streaming Service

## 📖 Описание проекта

**Multicast Streaming Service** — это сервис для потокового вещания видео, в котором:
- **Ядро сетевого взаимодействия написано на C++** в виде библиотеки `multicast_core`.
- **Графический интерфейс реализован на Python** с использованием Python-биндингов к C++ функциям через `pybind11`.

Проект позволяет передавать видеопоток через multicast по сети и принимать его на стороне клиентов с возможностью управления из Python GUI.

---

## 📂 Структура проекта
```bash
multicast_streaming_service/
├── gui/                          # Каталог для графического интерфейса на Python
│   └── main.py                   
├── multicast_core/               # Библиотека C++ для multicast передачи
│   ├── include/                  
│   │   ├── multicast_core_bits/  
│   │   │   ├── receiver.h        # Заголовок приемника данных
│   │   │   └── sender.h          # Заголовок отправителя данных
│   │   └── multicast_core.h      # Основной заголовок библиотеки
│   ├── src/                      
│   │   ├── receiver.cpp          # Реализация приёма данных
│   │   └── sender.cpp            # Реализация отправки данных
│   ├── tests/                    # Каталог с тестами для ядра
│   │   ├── src/                  
│   │   │   └── test.cpp          
│   │   └── CMakeLists.txt        # cmake для сборки тестов библиотеки
│   └── CMakeLists.txt            # cmake-скрипт для сборки С++ библиотеки
├── pybindings/                   # Биндинги для Python с использованием pybind11
│   ├── multicast_core.cpp       
│   ├── receiver.cpp            
│   └── sender.cpp                
├── CMakeLists.txt                # cmake-скрипт для сборки python-модуля
├── ProjectConfig.cmake           # Конфигурация CMake
└── README.md                    

```
---

## 🛠 Технологии

- **C++17**
- **Python3**
- **Pybind11**
- **CMake**
- **Ninja / Make**
- **Multicast (UDP)**

---

## 📦 Сборка проекта

### Требования:
- CMake ≥ 3.16
- Python ≥ 3.8
- Ninja или Make
- GCC / Clang

Перед сборкой и установкой библиотеки нужно указать необходимые переменные в файле `ProjectConfig.cmake`:
- `CPP_LIB_INSTALL_DIR` - путь, куда будет установлена библиотека C++
- `PYTHON_EXECUTABLE` - путь до интерпретатора python
- `PYTHON_LIB_INSTALL_DIR` - путь, куда будет установлен python-пакет, можно установить путь до ваших python site-packages

---

### Сборка C++ библиотеки:
```bash
cd multicast_core
mkdir build && cd build
cmake ..
make && sudo make install
```
### Запуск тестов C++ библиотеки:
После успешной установки библиотеки можно скомпилировать и запустить тесты:
```bash
cd multicast_core/tests
mkdir build && cd build
cmake .. && make
../bin/test
```

---

### Сборка python-модуля:
```bash
mkdir build && cd build
cmake ..
make && sudo make install
```

### 🚀 Запуск GUI
После сборки:
```bash
python gui/main.py
```
Если в качестве пути установки модуля был установлен ваш python site-packages, интерпретатор автоматически обнаружит модуль, и он будет доступен из **любого** python-скрипта