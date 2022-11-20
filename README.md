# flutter_internationalization

A new Flutter project.

## Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://docs.flutter.dev/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://docs.flutter.dev/cookbook)

For help getting started with Flutter development, view the
[online documentation](https://docs.flutter.dev/), which offers tutorials,
samples, guidance on mobile development, and a full API reference.


## Comandos 

flutter analyze
flutter test
flutter run


## Internacionalización 

1. Asegurarse que los paquetes estén instalados agregándolos en el archivo `pubspec.yaml`

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_localizations:
    sdk: flutter
  intl: ^0.17.0

flutter:
  generate: true
```

2. Creamos el archivo `l10n.yaml` en la raíz del proyecto
con la siguiente información 

```yaml
arb-dir: lib/l10n
template-arb-file: app_en.arb
output-localization-file: app_localizations.dart
```

- `arb-dir` especifica el directorio donde se van a guardar los archivos de configuración para las traducciones.
- `template-arb-file` es el template que define todos los mensajes que va manejar la aplicación.
- `output-localization-file` define la clase dart que se genera para las traducciones el cual al compilar se crea en `.dart_tool/flutter_gen/gen_l10n`.

3. Creamos el archivo ARB `app_en.arb`, en el directorio `l10n`en caso de no existir crearlo `lib/l10n/app_en.arb`.

4. Colocamos dentro del archivo `app_en.arb` una estructura como la siguiente:
```JSON
{
  "@@locale": "en",

  "helloWorld": "Hello World!",
  "@helloWorld": {
    "description": "The conventional newborn programmer greeting"
  }
}
```

5. Podemos agregar más archivos ARB para traducción a otro idioma por ejemplo español `lib/l10n/app_es.arb`

6. Dentro del archivo agregar el mensaje

```JSON
{
    "helloWorld": "¡Hola Mundo!"
}
```

7. Ahora, ejecutemos `flutter gen-l10n` para que se generen los archivos transpilados a DART. Los archivos generados debería poder verlos en `.dart_tool/flutter_gen/gen_l10n`. Cada que se agregue un nuevo mensaje es necesario volver a ejecutar el comando.

8. Puede realizar la configuración de cualquiera de las siguientes maneras:


  1. Agregar AppLocalizations.delegate dentro de la propiedad localizationsDelegates de MaterialApp.

  ```dart
  // Agregar este import
  import 'package:flutter_gen/gen_l10n/app_localizations.dart';
  ```

  ```dart
  return const MaterialApp(
    title: 'Flutter App',
    localizationsDelegates: [
      AppLocalizations.delegate, // Agregar esta línea
      GlobalMaterialLocalizations.delegate,
      GlobalWidgetsLocalizations.delegate,
      GlobalCupertinoLocalizations.delegate,
    ],
    supportedLocales: [
      Locale('en', ''), 
      Locale('es', ''), 
    ],
    home: MyHomePage(),
  );
  ```
  2. También puede usar los localizationsDelegates y supportedLocales generados en l10n, así evita colocarlos manualmente, como en el paso anterior.

  ```dart
  const MaterialApp(
    title: 'Flutter App',
    localizationsDelegates: AppLocalizations.localizationsDelegates,
    supportedLocales: AppLocalizations.supportedLocales,
  );
  ```

9. Para utilizar los mensajes creados, se puede hacer de la siguiente manera:

```dart
Text(AppLocalizations.of(context)!.helloWorld);
```

10. Si trabajan con Visual studio code, recomendable instalar el plugin [Flutter Intl](https://marketplace.visualstudio.com/items?itemName=localizely.flutter-intl)


## Región actual


Con Locale `myLocale = Localizations.localeOf(context);` puede obtener siempre la región actual de su dispositivo.

## Fuentes para configuración de internalización


- [Documento de guía](https://docs.google.com/document/d/10e0saTfAv32OZLRmONy866vnaw0I2jwL8zukykpgWBc/edit#heading=h.w1agvlp3evhy)
- [Documentación Flutter](https://docs.flutter.dev/development/accessibility-and-localization/internationalization)
