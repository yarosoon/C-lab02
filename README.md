# Csharp_lab02
## Цели работы:
  1. Научиться синтаксису и основным принципам наследования в C#.
## Задание №1
Создайте класс, представляющий учебный класс ClassRoom.
Создайте класс ученик - Pupil. 
В теле класса создайте методы void Study(), void Read(), void Write(), void Relax().
Создайте 3 производных класса ExcelentPupil, GoodPupil, BadPupil от класса базового класса Pupil и переопределите каждый из методов, в зависимости от успеваемости ученика (реализация может быть произвольной, например простой вывод на консоль разных строк).
Конструктор класса ClassRoom принимает аргументы типа Pupil, класс должен состоять из 4 учеников.
Предусмотрите возможность того, что пользователь может передать 2 или 3 аргумента.
Выведите информацию о том, как все ученики экземпляра класса ClassRoom умеют учиться, читать, писать, отдыхать. 

Примечание: при реализации возможности создания экземпляра класса ClassRoom с произвольным количеством учеников воспользуйтесь ключевым словом params.

## Задание№2
Создайте класс Vehicle.
В теле класса создайте поля: координаты и параметры средств передвижения (цена, скорость, год выпуска).
Создайте 3 производных класса Plane, Саг и Ship.
Для класса Plane должна быть определена высота и количество пассажиров.
Для класса Ship — количество пассажиров и порт приписки.
Написать программу, которая выводит на экран информацию о каждом средстве передвижения.

Примечание: избегайте дублирования кода, используйте ключевое слово base после объявления конструкторов в классах наследниках для вызова и передачи параметров в конструктор базового класса.

## Задание №3
Создайте класс DocumentWorker.
В теле класса создайте три метода OpenDocument(), EditDocument(), SaveDocument().
В тело каждого из методов добавьте вывод на экран соответствующих строк: "Документ открыт", "Редактирование документа доступно в версии Pro", "Сохранение документа доступно в версии Pro".
Создайте производный класс ProDocumentWorker.
Переопределите соответствующие методы, при переопределении методов выводите следующие строки: "Документ отредактирован", "Документ сохранен в старом формате, сохранение в остальных форматах доступно в версии Expert".
Создайте производный класс ExpertDocumentWorker от базового класса ProDocumentWorker.
Переопределите соответствующий метод. При вызове данного метода необходимо выводить на экран "Документ сохранен в новом формате".
В теле метода Main() реализуйте возможность приема от пользователя номера ключа доступа pro и exp.
Если пользователь не вводит ключ, он может пользоваться только бесплатной версией (создается экземпляр базового класса), если пользователь ввел номера ключа доступа pro и exp, то должен создаться экземпляр соответствующей версии класса, приведенный к базовому – DocumentWorker.

## Код задания № 1
    using System;
    
    namespace School
    {
        // Базовый класс ученик
        class Pupil
        {
            public virtual void Study() => Console.WriteLine("Pupil is studying."); // Используем virtual, чтобы производный класс мог использовать модификатор override для переопределения методов
            public virtual void Read() => Console.WriteLine("Pupil is reading."); // Используем virtual, чтобы производный класс мог использовать модификатор override для переопределения методов
            public virtual void Write() => Console.WriteLine("Pupil is writing."); // Используем virtual, чтобы производный класс мог использовать модификатор override для переопределения методов
            public virtual void Relax() => Console.WriteLine("Pupil is relaxing."); // Используем virtual, чтобы производный класс мог использовать модификатор override для переопределения методов
        }
    
        // Отличник
        class ExcelentPupil : Pupil
        {
            public override void Study() => Console.WriteLine("Excelent pupil studies excellently."); // Переопределяем методы
            public override void Read() => Console.WriteLine("Excelent pupil reads quickly and comprehensively."); // Переопределяем методы
            public override void Write() => Console.WriteLine("Excelent pupil writes neatly and precisely."); // Переопределяем методы
            public override void Relax() => Console.WriteLine("Excelent pupil rarely relaxes, but does it effectively."); // Переопределяем методы
        }
    
        // Хорошист
        class GoodPupil : Pupil
        {
            public override void Study() => Console.WriteLine("Good pupil studies well."); // Переопределяем методы
            public override void Read() => Console.WriteLine("Good pupil reads at a good pace."); // Переопределяем методы
            public override void Write() => Console.WriteLine("Good pupil writes well."); // Переопределяем методы 
            public override void Relax() => Console.WriteLine("Good pupil knows when to relax."); // Переопределяем методы
        }
    
        // Троечник
        class BadPupil : Pupil
        {
            public override void Study() => Console.WriteLine("Bad pupil studies poorly."); // Переопределяем методы
            public override void Read() => Console.WriteLine("Bad pupil reads reluctantly."); // Переопределяем методы
            public override void Write() => Console.WriteLine("Bad pupil writes with many mistakes."); // Переопределяем методы
            public override void Relax() => Console.WriteLine("Bad pupil relaxes most of the time."); // Переопределяем методы
        }
    
        // Учебный класс
        class ClassRoom
        {
            private Pupil[] pupils;
    
            public ClassRoom(params Pupil[] pupils)
            {
                // Если передано меньше 4 учеников, заполняем оставшиеся позиции null
                this.pupils = new Pupil[4];
                for (int i = 0; i < pupils.Length && i < 4; i++)
                {
                    this.pupils[i] = pupils[i];
                }
    
                // Заполняем оставшиеся ученики пустыми Pupil
                for (int i = pupils.Length; i < 4; i++)
                {
                    this.pupils[i] = new Pupil();
                }
            }
    
            public void ShowPupilSkills()
            {
                for (int i = 0; i < pupils.Length; i++)
                {
                    Console.WriteLine($"Pupil {i + 1}:");
                    pupils[i].Study();
                    pupils[i].Read();
                    pupils[i].Write();
                    pupils[i].Relax();
                    Console.WriteLine();
                }
            }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                // Создаем учеников
                Pupil excelentPupil = new ExcelentPupil();
                Pupil goodPupil = new GoodPupil();
                Pupil badPupil = new BadPupil();
    
                // Создаем учебный класс, передавая 3 ученика, 4-й заполняется по умолчанию
                ClassRoom classRoom = new ClassRoom(excelentPupil, goodPupil, badPupil);
    
                // Выводим информацию об учениках
                classRoom.ShowPupilSkills();
            }
        }
    }
## Код задания № 2
    using System;
    
    class Vehicle
    {
        // Поля для координат и параметров транспортных средств
        public double X { get; set; }
        public double Y { get; set; }
        public double Price { get; set; }
        public double Speed { get; set; }
        public int YearOfManufacture { get; set; }
    
        // Конструктор базового класса
        public Vehicle(double x, double y, double price, double speed, int yearOfManufacture)
        {
            X = x;
            Y = y;
            Price = price;
            Speed = speed;
            YearOfManufacture = yearOfManufacture;
        }
    
        // Метод для отображения информации о транспортном средстве
        public virtual void DisplayInfo()
        {
            Console.WriteLine($"Координаты: ({X}, {Y})\nЦена: {Price}\nСкорость: {Speed}\nГод выпуска: {YearOfManufacture}");
        }
    }
    
    // Производный класс Plane
    class Plane : Vehicle
    {
        public double Height { get; set; }
        public int NumberOfPassengers { get; set; }
    
        // Конструктор для класса Plane, использует конструктор базового класса
        public Plane(double x, double y, double price, double speed, int yearOfManufacture, double height, int numberOfPassengers)
            : base(x, y, price, speed, yearOfManufacture) // Вызов конструктора базового класса Vehicle из конструктора производного класса Plane
        {
            Height = height;
            NumberOfPassengers = numberOfPassengers;
        }
    
        // Переопределение метода для отображения дополнительной информации
        public override void DisplayInfo()
        {
            base.DisplayInfo(); // Вызов метода DisplayInfo() из базового(родительского) класса
            Console.WriteLine($"Высота: {Height}\nКоличество пассажиров: {NumberOfPassengers}");
        }
    }
    
    // Производный класс Car
    class Car : Vehicle
    {
        public Car(double x, double y, double price, double speed, int yearOfManufacture)
            : base(x, y, price, speed, yearOfManufacture) // Вызов конструктора базового класса Vehicle из конструктора производного класса Car
        {
        }
    }
    
    // Производный класс Ship
    class Ship : Vehicle
    {
        public int NumberOfPassengers { get; set; }
        public string PortOfRegistry { get; set; }
    
        // Конструктор для класса Ship, использует конструктор базового класса
        public Ship(double x, double y, double price, double speed, int yearOfManufacture, int numberOfPassengers, string portOfRegistry)
            : base(x, y, price, speed, yearOfManufacture) // Вызов конструктора базового класса Vehicle из конструктора производного класса Ship
        {
            NumberOfPassengers = numberOfPassengers;
            PortOfRegistry = portOfRegistry;
        }
    
        // Переопределение метода для отображения дополнительной информации
        public override void DisplayInfo()
        {
            base.DisplayInfo(); // Вызов метода DisplayInfo() из базового(родительского) класса
            Console.WriteLine($"Количество пассажиров: {NumberOfPassengers}\nПорт приписки: {PortOfRegistry}");
        }
    }
    
    class Program
    {
        static void Main(string[] args)
        {
            // Создание экземпляров производных классов
            Plane plane = new Plane(100, 200, 500000, 800, 2020, 10000, 150);
            Car car = new Car(50, 50, 30000, 150, 2022);
            Ship ship = new Ship(70, 80, 1000000, 50, 2018, 300, "Москва");
    
            // Отображение информации о каждом средстве передвижения
            Console.WriteLine("Информация о самолете:");
            plane.DisplayInfo();
            Console.WriteLine("\nИнформация о автомобиле:");
            car.DisplayInfo();
            Console.WriteLine("\nИнформация о корабле:");
            ship.DisplayInfo();
        }
    }
## Код задания № 3
    using System;
    
    namespace DocumentWorkerApp
    {
        class DocumentWorker
        {
            public virtual void OpenDocument()
            {
                Console.WriteLine("Документ открыт");
            }
    
            public virtual void EditDocument()
            {
                Console.WriteLine("Редактирование документа доступно в версии Pro");
            }
    
            public virtual void SaveDocument()
            {
                Console.WriteLine("Сохранение документа доступно в версии Pro");
            }
        }
    
        class ProDocumentWorker : DocumentWorker
        {
            public override void EditDocument()
            {
                Console.WriteLine("Документ отредактирован");
            }
    
            public override void SaveDocument()
            {
                Console.WriteLine("Документ сохранен в старом формате, сохранение в остальных форматах доступно в версии Expert");
            }
        }
    
        class ExpertDocumentWorker : ProDocumentWorker
        {
            public override void SaveDocument()
            {
                Console.WriteLine("Документ сохранен в новом формате");
            }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                // Задаём пароль
                const string proKey = "pro123";
                const string expKey = "exp123";
    
                Console.WriteLine("Введите ключ доступа (pro/exp): ");
                string key = Console.ReadLine();
    
                DocumentWorker documentWorker;
    
                if (key == proKey)
                {
                    documentWorker = new ProDocumentWorker();
                }
                else if (key == expKey)
                {
                    documentWorker = new ExpertDocumentWorker();
                }
                else
                {
                    documentWorker = new DocumentWorker();
                }
    
                // Демонстрация работы
                documentWorker.OpenDocument();
                documentWorker.EditDocument();
                documentWorker.SaveDocument();
    
                Console.ReadKey();
            }
        }
    }

C# lab02
