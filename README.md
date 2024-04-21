# Context Menu for Filament

[![Latest Version on Packagist](https://img.shields.io/packagist/v/aymanalhattami/filament-context-menu.svg?style=flat-square)](https://packagist.org/packages/aymanalhattami/filament-context-menu)
[![GitHub Tests Action Status](https://img.shields.io/github/actions/workflow/status/aymanalhattami/filament-context-menu/run-tests.yml?branch=main&label=tests&style=flat-square)](https://github.com/aymanalhattami/filament-context-menu/actions?query=workflow%3Arun-tests+branch%3Amain)
[![GitHub Code Style Action Status](https://img.shields.io/github/actions/workflow/status/aymanalhattami/filament-context-menu/fix-php-code-styling.yml?branch=main&label=code%20style&style=flat-square)](https://github.com/aymanalhattami/filament-context-menu/actions?query=workflow%3A"Fix+PHP+code+styling"+branch%3Amain)
[![Total Downloads](https://img.shields.io/packagist/dt/aymanalhattami/filament-context-menu.svg?style=flat-square)](https://packagist.org/packages/aymanalhattami/filament-context-menu)

---
This package is used to add context menu (right click menu) for resource pages and custom pages of [Filament Admin Panel](https://filamentphp.com/).
* It uses [Filament Actions](https://filamentphp.com/docs/3.x/actions/overview) to set menu items.
* Support dark and light mode.
* Support left-to-right and right-to-left direction.
* You can set a divider between menu actions.

[Demo project](https://github.com/aymanalhattami/filament-context-menu-project)

## Installation

You can install the package via composer:

```bash
composer require aymanalhattami/filament-context-menu
```

## Usage
1. Add the trait ```AymanAlhattami\FilamentContextMenu\InteractsWithContextMenuActions``` to the page you want to add context menu.
2. Then, define a ```getContextMenuActions``` method inside the page, the method should return an array of [Filament Actions](https://filamentphp.com/docs/3.x/actions/installation)

```php
use App\Filament\Resources\UserResource\Pages\CreateUser;
use Filament\Resources\Pages\ListRecords;
use AymanAlhattami\FilamentContextMenu\ContextMenu;
use Filament\Actions\Action;
use AymanAlhattami\FilamentContextMenu\InteractsWithContextMenuActions;

class ListUsers extends ListRecords
{
    use InteractsWithContextMenuActions;
    
    public function getContextMenuActions(): array
    {
        return [
            Action::make('Create user')
                ->url(CreateUser::getUrl())
        ];
    }
    
    // 
}
```

## More options

### Divider
Use ```AymanAlhattami\FilamentContextMenu\ContextMenuDivider``` to set divider between menu actions
```php
use App\Filament\Resources\UserResource\Pages\CreateUser;
use App\Filament\Resources\UserResource\Pages\TrashedUsers;
use Filament\Resources\Pages\ListRecords;
use Filament\Actions\Action;
use AymanAlhattami\FilamentContextMenu\ContextMenuDivider;
use AymanAlhattami\FilamentContextMenu\InteractsWithContextMenuActions;

class ListUsers extends ListRecords
{
    use InteractsWithContextMenuActions;

    // 
    
    public static function getContextMenuActions(): array
    {
        return [
            Action::make('Create user')
                ->url(CreateUser::getUrl()),
            ContextMenuDivider::make(),
            Action::make('Trashed user')
                ->url(TrashedUsers::getUrl()),
        ];
    }
    
    // 
}
```

### Create Action
You can use ```Filament\Actions\CreateAction```, visit [filament create action](https://filamentphp.com/docs/3.x/actions/prebuilt-actions/create) for more information.

```php
use Filament\Resources\Pages\ListRecords;
use AymanAlhattami\FilamentContextMenu\ContextMenuDivider;
use AymanAlhattami\FilamentContextMenu\InteractsWithContextMenuActions;

class ListUsers extends ListRecords
{
    use InteractsWithContextMenuActions;

    // 
    
    public static function getContextMenuActions(): array
    {
        return [
            \Filament\Actions\CreateAction::make()
                ->model(App\Models\User::class)
                 ->form([
                    TextInput::make('name')
                        ->required(),
                    // ...
                ])
        ];
    }
    
    // 
}
```

### Edit Action
You can use ```Filament\Actions\EditAction```, visit [filament edit action](https://filamentphp.com/docs/3.x/actions/prebuilt-actions/edit) for more information.

```php
use Filament\Resources\Pages\ViewRecord;
use AymanAlhattami\FilamentContextMenu\ContextMenu;
use AymanAlhattami\FilamentContextMenu\InteractsWithContextMenuActions;

class ViewUser extends ViewRecord
{
    use InteractsWithContextMenuActions;

    // 
    
    public static function getContextMenuActions(): array
    {
        return [
            \Filament\Actions\EditAction::make()
                ->record($this->user)
                ->form([
                    TextInput::make('name')
                        ->required(),
                    // ...
                ])
        ];
    }
    
    // 
}
```

### View Action
You can use ```Filament\Actions\ViewAction```, visit [filament view action](https://filamentphp.com/docs/3.x/actions/prebuilt-actions/view) for more information.

```php
use Filament\Resources\Pages\EditRecord;
use AymanAlhattami\FilamentContextMenu\ContextMenu;
use AymanAlhattami\FilamentContextMenu\InteractsWithContextMenuActions;

class EditUser extends EditRecord
{
    use InteractsWithContextMenuActions;

    // 
    
    public static function getContextMenuActions(): array
    {
        return [
            \Filament\Actions\ViewAction::make()
                ->record($this->user)
                 ->form([
                    TextInput::make('name')
                        ->required(),
                    // ...
                ])
                
        ];
    }
    
    // 
}
```

### Delete Action
You can use  ```Filament\Actions\DeleteAction```, visit [filament delete action](https://filamentphp.com/docs/3.x/actions/prebuilt-actions/delete) for more information.

```php
use Filament\Resources\Pages\ViewRecord;
use AymanAlhattami\FilamentContextMenu\ContextMenu;
use AymanAlhattami\FilamentContextMenu\InteractsWithContextMenuActions;

class ViewUser extends ViewRecord
{
    use InteractsWithContextMenuActions;

    // 
    
    public static function getContextMenuActions(): array
    {
        return [
            \Filament\Actions\DeleteAction::make()
                ->record($this->user)
        ];
    }
    
    // 
}
```

### Replicate Action
You can use  ```Filament\Actions\ReplicateAction```, visit [filament replicate action](https://filamentphp.com/docs/3.x/actions/prebuilt-actions/replicate) for more information.

```php
use Filament\Resources\Pages\ViewRecord;
use AymanAlhattami\FilamentContextMenu\ContextMenu;
use AymanAlhattami\FilamentContextMenu\InteractsWithContextMenuActions;

class ViewUser extends ViewRecord
{
    use InteractsWithContextMenuActions;

    // 
    
    public static function getContextMenuActions(): array
    {
        return [
            \Filament\Actions\ReplicateAction::make()
                ->record($this->user)
        ];
    }
    
    // 
}
```

### Force Delete Action
You can use ```Filament\Actions\ForceDeleteAction```, visit [filament force delete action](https://filamentphp.com/docs/3.x/actions/prebuilt-actions/force-delete) for more information.

```php
use Filament\Resources\Pages\ViewRecord;
use AymanAlhattami\FilamentContextMenu\ContextMenu;
use AymanAlhattami\FilamentContextMenu\InteractsWithContextMenuActions;

class ViewUser extends ViewRecord
{
    use InteractsWithContextMenuActions;

    // 
    
    public static function getContextMenuActions(): array
    {
        return [
            \Filament\Actions\ForceDeleteAction::make()
                ->record($this->user)
        ];
    }
    
    // 
}
```

### Restore Action
You can use ```Filament\Actions\RestoreAction```, visit [filament restore action](https://filamentphp.com/docs/3.x/actions/prebuilt-actions/restore) for more information.

```php
use Filament\Resources\Pages\ListRecords;
use AymanAlhattami\FilamentContextMenu\ContextMenu;
use AymanAlhattami\FilamentContextMenu\InteractsWithContextMenuActions;

class ListUsers extends ListRecords
{
    use InteractsWithContextMenuActions;

    // 
    
    public static function getContextMenuActions(): array
    {
        return [
            \Filament\Actions\RestoreAction::make()
                ->record($this->user)
        ];
    }
    
    // 
}
```

### Import Action
You can use ```Filament\Actions\ImportAction```, visit [filament import action](https://filamentphp.com/docs/3.x/actions/prebuilt-actions/import) for more information.

```php
use Filament\Resources\Pages\ListRecords;
use AymanAlhattami\FilamentContextMenu\ContextMenu;
use AymanAlhattami\FilamentContextMenu\InteractsWithContextMenuActions;
use App\Filament\Imports\UserImporter;

class ListUsers extends ListRecords
{
    use InteractsWithContextMenuActions;

    // 
    
    public static function getContextMenuActions(): array
    {
        return [
            \Filament\Actions\ImportAction::make()
                ->importer(UserImporter::class)
        ];
    }
    
    // 
}
```

### Export Action
You can use ```Filament\Actions\ExportAction```, visit [filament export action](https://filamentphp.com/docs/3.x/actions/prebuilt-actions/export) for more information.

```php
use Filament\Resources\Pages\ListRecords;
use AymanAlhattami\FilamentContextMenu\ContextMenu;
use AymanAlhattami\FilamentContextMenu\InteractsWithContextMenuActions;
use App\Filament\Exports\UserExporter;

class ListUsers extends ListRecords
{
    use InteractsWithContextMenuActions;

    // 
    
    public static function getContextMenuActions(): array
    {
        return [
            \Filament\Actions\ExportAction::make()
                ->exporter(UserExporter::class)
        ];
    }
    
    // 
}
```

### Note 
For action to have a nice style, use ```->link()``` method a the action, [link](https://filamentphp.com/docs/3.x/actions/trigger-button#choosing-a-trigger-style)
 
```php
public static function getContextMenuActions(): array
{
    return [
        Action::make('Create user')
            ->url(CreateUser::getUrl())
            ->link()
        ];
}
```

## Testing

```bash
composer test
```

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

## Contributing

Please see [CONTRIBUTING](.github/CONTRIBUTING.md) for details.

## Security Vulnerabilities

Please review [our security policy](../../security/policy) on how to report security vulnerabilities.

## Credits

- [aymanalhattami](https://github.com/aymanalhattami)
- [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
