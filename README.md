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

Agora é só importar no model e ser feliz :)


```
class Cliente extends Model
{
    use HasFactory, HasPrimaryKeyUuid;
    protected $table = 'clientes';
    
}
```


https://www.youtube.com/watch?v=7N2mFbKhq_M 
