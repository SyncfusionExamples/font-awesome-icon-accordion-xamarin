# font-awesome-icon-accordion-xamarin

This sample demonstrates how to use Font Awesome icons inside the headers of a Syncfusion SfAccordion control in Xamarin.Forms. It illustrates a practical pattern where each accordion header displays a text label along with a Font Awesome glyph (as a Button.ImageSource using a `FontImageSource`).

For background on the Accordion control, see the official user guide:

- [Getting started with Xamarin Accordion (SfAccordion)](https://help.syncfusion.com/xamarin/accordion/getting-started)

KB Link: [How to use Font Awesome icons in Xamarin.Forms Accordion (SfAccordion)](https://www.syncfusion.com/kb/12188/how-to-use-font-awesome-icons-in-xamarin-forms-accordion-sfaccordion)

## Overview
The `SfAccordion` control provides a list of expandable items where each `AccordionItem` can contain arbitrary Header and Content templates. In this sample the header is built as a simple Grid that contains a text `Label` and a `Button` whose `ImageSource` is a `FontImageSource` that uses a Font Awesome font family. The `BindableLayout.ItemsSource` is used to create items from a VM collection (`Info`). The button is bound to a command on the accordion's `BindingContext` to toggle a favourite action.

The key points are:
- Use `BindableLayout.ItemsSource` to bind the accordion to a collection.
- Provide a `DataTemplate` that defines `AccordionItem.Header` and `AccordionItem.Content`.
- Use a `FontImageSource` inside a `Button.ImageSource` to render Font Awesome glyphs.
- Reference the accordion's `BindingContext` for shared commands using `Source={x:Reference accordion}`.

## XAML
The following snippet is taken from the sample `MainPage.xaml` and shows the essential parts of the header and content templates used in this project.

```
<ContentPage.BindingContext>
	<local:ItemInfoRepository/>
</ContentPage.BindingContext>

<ContentPage.Resources>
	<ResourceDictionary>
		<OnPlatform x:TypeArguments="x:String" x:Key="FontAwesome">
			<On Platform="Android" Value="FontAwesomeRegular.otf#Regular" />
			<On Platform="iOS" Value="FontAwesome5Free-Regular" />
			<On Platform="UWP" Value="/Assets/FontAwesomeRegular.otf#Font Awesome 5 Free" />
		</OnPlatform>
	</ResourceDictionary>
</ContentPage.Resources>

<ContentPage.Content>
	<accordion:SfAccordion x:Name="accordion" BindableLayout.ItemsSource="{Binding Info}" ExpandMode="SingleOrNone" HeaderIconPosition="Start">
		<BindableLayout.ItemTemplate>
			<DataTemplate>
				<accordion:AccordionItem >
					<accordion:AccordionItem.Header>
						<Grid>
							<Label TextColor="#495F6E" Text="{Binding Name}" VerticalOptions="Center" HorizontalOptions="StartAndExpand" HeightRequest="50" VerticalTextAlignment="Center"/>
							<Button Grid.Column="1" HeightRequest="50" WidthRequest="50" Command="{Binding Path=BindingContext.FavouriteCommand, Source={x:Reference accordion}}" CommandParameter="{Binding .}" HorizontalOptions="EndAndExpand" VerticalOptions="CenterAndExpand" BackgroundColor="Transparent">
								<Button.ImageSource>
									<FontImageSource Glyph="{Binding FavouriteIcon}" FontFamily="{StaticResource FontAwesome}" Color="#ea2c62" Size="18" />
								</Button.ImageSource>
							</Button>
						</Grid>
					</accordion:AccordionItem.Header>
					<accordion:AccordionItem.Content>
						<Grid BackgroundColor="#e8e8e8" Padding="5,0,0,0">
							<Label Text="{Binding Description}" VerticalOptions="Center"/>
						</Grid>
					</accordion:AccordionItem.Content>
				</accordion:AccordionItem>
			</DataTemplate>
		</BindableLayout.ItemTemplate>
	</accordion:SfAccordion>
</ContentPage.Content>
```

## How it works
- Font registration: the sample expects a Font Awesome font file included in platform projects (for example `FontAwesomeRegular.otf` in Android/UWP assets and the appropriate iOS registration) and maps it with an `OnPlatform` resource named `FontAwesome`.
- Glyph binding: each item in the view-model includes a `FavouriteIcon` property (a character/glyph string) that the `FontImageSource` uses as the `Glyph` to render the icon.
- Commands: the `FavouriteCommand` is defined on the page/view-model and is referenced from the item template via `Source={x:Reference accordion}` so the item-level binding can pass itself as `CommandParameter`.


##### Conclusion
I hope you enjoyed learning about how to use Font Awesome icons in Xamarin.Forms Accordion (SfAccordion).

You can refer to our  [Xamarin.Forms Accordion feature tour](https://www.syncfusion.com/xamarin-ui-controls/xamarin-accordion) page to know about its other groundbreaking feature representations and [documentation](https://help.syncfusion.com/xamarin/accordion/getting-started), and how to quickly get started for configuration specifications. You can also explore our [Xamarin.Forms Accordion example](https://www.syncfusion.com/demos/xamarin) to understand how to create and manipulate data.

For current customers, you can check out our Document Processing Libraries from the [License and Downloads](https://www.syncfusion.com/account/login) page. If you are new to Syncfusion, you can try our 30-day [free trial](https://www.syncfusion.com/downloads) to check out our controls.

If you have any queries or require clarifications, please let us know in the comments section below. You can also contact us through our [support forums](https://www.syncfusion.com/forums) or [Direct-trac](https://support.syncfusion.com/create). We are always happy to assist you!
