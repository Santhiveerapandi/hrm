## Installation
```
$ composer create-project --prefer-dist laravel/laravel hrm
$ cd hrm
$ npm install
$ npm list --json

# .env file DB configuration changes
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=hrm
DB_USERNAME=hrm
DB_PASSWORD=hrm@123
DB_PREFIX=hrm_

# config/database.php
'mysql' => [
    ....
    'prefix' => env('DB_PREFIX', 'hrm_'),


$ php artisan migrate

# Check Environment
$ php artisan about


$ php artisan env:encrypt

$ php artisan config:publish
```
## Laravel authentication
```
$ composer require laravel/ui
$ php artisan ui bootstrap
$ php artisan ui bootstrap --auth
$ npm install
$ npm run build
```

## Theme Integration
```
$ composer require jeroennoten/laravel-adminlte
$ php artisan adminlte:install
$ php artisan adminlte:install --only=auth_views
```

## Registered user email verification
```
## routes/web.php
// Add this to enable email verification routes
Auth::routes(['verify' => true]);

Route::middleware(['auth', 'verified'])->group(function () {
    Route::get('/home', [App\Http\Controllers\HomeController::class, 'index'])->name('home');
});
Route::post('email/verification-notification', [App\Http\Controllers\Auth\EmailVerificationNotificationController::class, 'store'])
    ->middleware(['auth', 'throttle:6,1'])
    ->name('verification.send');

-------------------
## app/Http/Controllers/Auth/EmailVerificationNotificationController.php

namespace App\Http\Controllers\Auth;

use App\Http\Controllers\Controller;
use Illuminate\Http\Request;

class EmailVerificationNotificationController extends Controller
{
    /**
     * Send a new email verification notification.
     *
     * @param  \Illuminate\Http\Request  $request
     * @return \Illuminate\Http\RedirectResponse
     */
    public function store(Request $request)
    {
        if ($request->user()->hasVerifiedEmail()) {
            return redirect()->intended('/home');
        }

        $request->user()->sendEmailVerificationNotification();

        return back()->with('status', 'verification-link-sent');
    }
}
```

## HMVC implementation
Reference [https://nwidart.com/laravel-modules/v6/installation-and-setup]

```
$ composer require nwidart/laravel-modules
$ php artisan vendor:publish --provider="Nwidart\Modules\LaravelModulesServiceProvider"
$ composer dump-autoload
```