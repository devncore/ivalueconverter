### About us

> &nbsp; :adult: __James Lee__ &nbsp;&nbsp; [Github](https://github.com/devncore-james) &nbsp;&nbsp; james.lee@devncore.org  
> &nbsp; :woman: __Elena Kim__ &nbsp;&nbsp; [Github](https://github.com/devncore-elena) &nbsp;&nbsp; elena.kim@devncore.org

We are very ordinary developers, so we need to communicate with you.   
You can always share information with us and we are looking forward to it.  

##### _Open Source &nbsp; https://github.com/devncore/devncore   &nbsp;&nbsp;   Official Website &nbsp; https://devncore.org_ 

### License Policy
[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)
[![GPLv3 license](https://img.shields.io/badge/License-GPLv3-blue.svg)](http://perso.crans.org/besson/LICENSE.html)

***

## IValueConverter

|Namespace|Assembly|
|:--------|:-------|
|`System.Windows.Data`|`PresentationFramework.dll`|

Value converters provides a way to apply custom logic to a [binding](https://github.com/devncore/wpf-xaml-binding).  
When source object type and target object type are different, value converters act like middlemen.  
Converter class must implement **IValueConverter** interface, which consists of two methods, `Convert()` and `ConvertBack()`.

_**Convert** method gets called when source updates target object._
```c#
public object Convert (object value, Type targetType, object parameter, CultureInfo culture);

// parameters:
//   value: The value produced by the binding source.
//   targetType: The type of the binding target property.
//   parameter: The converter parameter to use.
//   culture: The culture to use in the converter.
// return:
//   A converted value. If the method returns null, the valid null value is used.
```  

_**ConvertBack** method gets called when target updates source object._
```c#
public object ConvertBack (object value, Type targetType, object parameter, CultureInfo culture);

// parameters:
//   value: The value that is produced by the binding target.
//   targetType: The type to convert to.
//   parameter: The converter parameter to use.
//   culture: The culture to use in the converter.
// return:
//   A converted value. If the method returns null, the valid null value is used.
```  
***

## Sample
### BooleanToVisibilityConverter
##### `Converter.cs`
```c#
public class BooleanToVisibilityConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        return value.Equals(true) ? Visibility.Visible : Visibility.Collapsed;
    }

    public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
    {
        throw new NotImplementedException();
    }
}
```
##### `ConverterResource.xaml`
```xaml
<ResourceDictionary xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
                    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                    xmlns:cvt="clr-namespace:IValueConverterSample.Converters">
    <cvt:BooleanToVisibilityConverter x:Key="BooleanToVisibilityConverter"/>
</ResourceDictionary>
```
##### `Style`
```xaml
<Style TargetType="{x:Type TextBlock}" x:Key="TXB.HELLO">
    <Setter Property="Grid.Row" Value="0"/>
    <Setter Property="Text" Value="Hello!"/>
    <Setter Property="Foreground" Value="#EFE6D4"/>
    <Setter Property="FontWeight" Value="Bold"/>
    <Setter Property="FontSize" Value="18"/>
    <Setter Property="HorizontalAlignment" Value="Left"/>
    <Setter Property="Margin" Value="100 22 0 0"/>
    <Setter Property="Visibility" Value="{Binding ElementName=tgl, Path=IsChecked, 
  	  				  Converter={StaticResource BooleanToVisibilityConverter}}"/>
</Style>
```
##### `Result`
|`IsChecked`=true|`IsChecked`=false|
|----------------|-----------------|
|image1|image2|

### StringFormatConverter
##### `Converter.cs`
```csharp
public class StringFormatConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        return string.Format("{0:N0}%", value);
    }

    public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
    {
        throw new NotImplementedException();
    }
}
```
##### `ConverterResource.xaml`
```xaml
<ResourceDictionary xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
                    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                    xmlns:cvt="clr-namespace:IValueConverterSample.Converters">
    <cvt:StringFormatConverter x:Key="StringFormatConverter"/>
</ResourceDictionary>
```
##### `Style`
```xaml
...
<Style TargetType="{x:Type TextBlock}" x:Key="IN.CONTENT">
    <Setter Property="Grid.Column" Value="1"/>
    <Setter Property="Foreground" Value="#9B9688"/>
    <Setter Property="FontSize" Value="13"/>
    <Setter Property="FontWeight" Value="Bold"/>
    <Setter Property="HorizontalAlignment" Value="Left"/>
    <Setter Property="VerticalAlignment" Value="Center"/>
    <Setter Property="Margin" Value="10 20 0 0"/>
    <Setter Property="Text" Value="{Binding ElementName=slider2, Path=Value, Converter={StaticResource StringFormatConverter}}"/>
</Style>
...
```

##### `Result`
...

### MultiValueConverter

***

## Reference
[:bookmark_tabs:](https://www.codeproject.com/Tips/868163/IValueConverter-Example-and-Usage-in-WPF) **CODE PROJECT** &nbsp; <ins>IValueConverter Example and Usage in WPF</ins>  
[:bookmark_tabs:](https://docs.microsoft.com/en-ca/dotnet/api/system.windows.data.ivalueconverter?view=net-5.0) **Microsoft Docs** &nbsp; <ins>IValueConverter Interface</ins>  
[:bookmark_tabs:](https://www.wpf-tutorial.com/data-binding/value-conversion-with-ivalueconverter/) **WPF Tutorial** &nbsp; <ins>Value conversion with IValueConverter</ins>
