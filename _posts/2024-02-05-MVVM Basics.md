---
title: MVVM Basics
date: 2024-02-05 03:01:00 +0900
categories: [Object Oriented, Architecture Patterns]
tags: [mvvm, c#, wpf]     # TAG names should always be lowercase
---

## Understanding the Model-View-ViewModel Pattern

Modern application development prioritizes user experience and ease of maintenance.
Achieving these goals requires a structured and systematic approach, where the MVVM(Model-View-ViewModel) pattern plays a vital role.
Particularly favored in the .NET technology stack, MVVM clearly separates each component, facilitating development and maintenance.

### Basic Concepts of MVVM
* **Model**: Handles the application's data and business logic, including database queries, data validation, and transformation.
* **View**: The user interface(UI) that displays data to users and receives user inputs. In technologies like WPF or Xamarin.forms, the view defines design and layout using XAML.
* **ViewModel**: Acts as an intermediary between the View and Model. It prepares data from the Model for the View, making it easily consumable, and processes user inputs, issuing commands to the Model.

### Scope of MVVM
The MVVM pattern is widely used in various .NET-based platforms, including WPF, UWP(Universal Windows Platform), Xamarin, and the recent .NET MAUI(Multi-Platform App UI). These technologies all use XAML to define UI and offer advanced features for binding UI with data sources. MVVM also facilitates cross-platform development and enhances code reusability.

### Principles of MVVM
* **Data Binding**: One of the core principles of MVVM. It ensures that changes in the ViewModel's data are automatically reflected in the View, minimizing code-behind and enabling declarative UI definitions.
* **Command**: The ViewModel handles user actions(e.g., button clicks) through commands, defined within the ViewModel and executed without direct dependencies on the View.
* **Dependency Injection**: MVVM manages dependencies between the ViewModel and Model through dependency injection, simplifying testing and maintenance.


### Example
Let's create a simple "User Message Display" application using C# WPF with the MVVM pattern.
In this example, we'll implement functionality to store a message input by the user in the Model through the ViewModel and display the saved message in the View.

#### Step1. Configure the View
The View constructs the user interface. It includes a `TextBox` for user message input and a `TextBlock` to display the message.
Data binding is set up by binding the `DataContext` to `MessageViewModel`.

```xml
<Window x:Class="MvvmPractice.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MVVM Example" Height="200" Width="400">
    <StackPanel Margin="10">
        <TextBox Text="{Binding Message, UpdateSourceTrigger=PropertyChanged}" Height="20"/>
        <TextBlock Text="{Binding Message}" Margin="10,0"/>
    </StackPanel>
</Window>

```

#### Step2. Create the Model
The Model is responsible for the application's data and business logic.
In this example, we'll implement a simple message storage function.

```cs
public class Message {
    public string Message { get; set; }
}
```

#### Step3. Create the ViewModel
The ViewModel handles data processing and command execution between the View and Model. It implements the `INotifyPropertyChanged` interface to notify the View about data changes.

```cs
using System.ComponentModel;
public class MessageViewModel : INotifyPropertyChanged {
    private string _message;
    public string Message {
        get => _message;
        set {
            if(_message != value) {
                _message = value;
                OnPropertyChanged(nameof(Message));
            }
        }
    }

    public event PropertyChangedEventHandler PropertyChanged;

    protected virtual void OnPropertyChanged(string propertyName) {
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
}
```

#### Step4. Bind the ViewModel to the View
Modify the constructor in `MainWindow.xaml.cs` to create an instance of `MessageViewModel` and set it as the window's `DataContext`.
```cs
public partial class MainWindow : Window {
    public MainWindow() {
        InitializeComponent();
        DataContext = new MessageViewModel(); // Dependency Injection
    }
}
```
In this example, we've implemented a simple data-binding application using the basic components of the MVVM pattern.
The user inputs a message in the `TextBox`, which is stored in the `Message` Model through `MessageViewModel`.
The saved message is then displayed in the `TextBlock` via `MessageViewModel`.

During this process, whenever the `Message` property in the `MessageViewModel` changes, the `OnPropertyChanged` method is called to notify the View on the data change.
By using data binding, synchronization between UI elements and data is automatically managed.

The MVVM pattern thus reduces between the View and Model and clearly separates the responsibilities of each component, improving the maintainability and scalability of the application.

### Conclusion
The MVVM pattern is crucial is modern software development. 
It allows developers to clearly separate UI from business logic, creating applications that are easy to maintain and extend.

MVVM is particularly ideal for data-centric application and cross-platform development, continuing to play a significant role moving forward.

### Additional Resources
* [Microsoft Docs: Data binding overview](https://learn.microsoft.com/en-us/dotnet/desktop/wpf/data/?view=netdesktop-8.0#:~:text=Data%20binding%20is%20the%20process%20that%20establishes%20a,are%20bound%20to%20the%20data%20reflect%20changes%20automatically.)
* [Prism Library for WPF](https://prismlibrary.com/)