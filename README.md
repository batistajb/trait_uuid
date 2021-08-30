# trait_uuid
Trait UUID - Laravel

Crie uma pasta com nome de "Traits" dentro da pasta app. Depois na pasta crie a classe trait abaixo.

```
<?php

namespace App\Traits;

use Illuminate\Support\Str;

trait HasPrimaryKeyUuid
{
    /**
     *  Setup model event hooks.
     */
    public static function bootHasPrimaryKeyUuid()
    {
        static::creating(function ($model) {
            if (!$model->getKey()) {
                $model->{$model->getKeyName()} = Str::uuid()->toString();
            }
        });
    }

    /**
     * @return bool
     */
    public function getIncrementing()
    {
        return false;
    }

    /**
     * @return string
     */
    public function getKeyType()
    {
        return 'string';
    }
}
```



Lembre-se de ajustar seu banco de dados(migration).


```
public function up()
    {
        Schema::create('users', function (Blueprint $table) {
            $table->id();
            $table->uuid('uuid')->primary(); // Aqui
            $table->string('name');
            $table->string('email')->unique();
            $table->timestamp('email_verified_at')->nullable();
            $table->string('password');
            $table->rememberToken();
            $table->timestamps();
        });
    }

```


```
class Cliente extends Model
{
    use HasFactory, HasPrimaryKeyUuid;
    protected $table = 'clientes';
    
}
```


Agora é só importar no model e ser feliz :)


```
class Cliente extends Model
{
    use HasFactory, HasPrimaryKeyUuid;
    protected $table = 'clientes';
    
}
```


https://www.youtube.com/watch?v=7N2mFbKhq_M 
