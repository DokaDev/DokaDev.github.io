---
title: Event Binding in MVVM
date: 2024-02-06 20:01:00 +0900
categories: [Object Oriented, Architecture Patterns]
tags: [mvvm, c#, wpf]     # TAG names should always be lowercase
---
> Using ICommand and RelayCommand in WPF
{: .prompt-tip }

In the last post, we explored the basics of the MVVM pattern along with a simple implementation of data binding.
This time, we will focus on event binding within the MVVM pattern and look at how to handle user events in a WPF application.
Specifically, through an example using the `ICommand` interface and the `RelayCommand` class, we'll see how UI events like button clicks can be handled in the ViewModel.

## Event Binding and the ICommand Interface
Event Binding is a method for handling events(e.g., button clicks) of user interface elements.
In the MVVM pattern, `ICommand` interface is used to link events between the View and ViewModel.
The `ICommand` interface in WPF implements the Command pattern, providing `Execute` and `CanExecute` methods.
This allows the encapsulation and management of UI event logic in the ViewModel.

### Implementing the RelayCommand Class
`RelayCommand` is an implementation of the `ICommand` interface that allows for concise execution logic using lambda expressions or methods.
Here is a basic example of implementing the `RelayCommand`:

```cs
public class RelayCommand(Action<object> execute, Predicate<object> canExecute = null) : ICommand {
    public event EventHandler CanExecuteChanged {
        add { CommandManager.RequerySuggested += value; }
        remove { CommandManager.RequerySuggested -= value; }
    }

    public bool CanExecute(object? parameter) {
        return canExecute == null || canExecute(parameter);
    }

    public void Execute(object? parameter) {
        execute(parameter);
    }
}
```

## Example: Handling Button Click Events
Let's look at a simple example of using `RelayCommand` to handle button click events.
Our goals is to execute a specific method in the ViewModel when the user clicks a button.

### Step1. Setting up the ViewModel
First, we define an instance of `RelayCommand` in the ViewModel and the method that will be executed through this instance.

```cs
public class MainViewModel {
    public ICommand MyCommand { get; private set; }

    public MainViewModel() {
        MyCommand = new RelayCommand(ExecuteMethod);
    }

    private void ExecuteMethod() {
        MessageBox.Show("The button was clicked!");
    }
}
```

### Step2. Command Binding in the View
Now, in XAML, we bind the button's `Command` property to the `MyCommand` property in `MainViewModel`
```xml
<Window x:Class="MvvmPractice.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MVVM Example" Height="200" Width="400"
        DataContext="{StaticResource MainViewModel}">
    <Grid>
        <Button Command="{Binding MyCommand}" Content="Click Me" />
    </Grid>
</Window>
```

### Step3. Settin the DataContext
Finally, in `MainWindow.xaml.cs`, set the window's `DataContext` to an instance of `MainViewModel`.
```cs
public partial class MainWindow : Window {
    public MainWindow() {
        InitializeComponent();
        DataContext = new MainViewModel();
    }
}
```

This example shows that within the MVVM pattern, it is possible to use the `ICommand` interface and the `RelayCommand` class to handle UI element events in the ViewModel.
This approach reduces coupling between the View and ViewModel, enhancing code reusability and maintainability.

## Conclusion
In this post, we looked at event binding within the MVVM pattern, including how to implement and use the `ICommand` interface and `RelayCommand` class.
This allows for efficient handling of user events, enabling the development of cleaner and more maintainable WPF application.
MVVM goes beyond a structural pattern, playing a vital role in improving the development process and application quality.