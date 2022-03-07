# Model範例
```
<?php
 
namespace App\Models;
 
use Illuminate\Database\Eloquent\Model;
 
class Flight extends Model
{
    預設將class名稱轉為snake_case命名方式+複數名稱
    例: 
        class = ProductItem
        $table = product_items
    /**
     * 對應的table
     *
     * @var string
     */
    protected $table = 'flights';

    /**
     * 對應的主鍵
     *
     * @var string
     */
    protected $primaryKey = 'id';

    /**
     * 主鍵是否自動遞增
     *
     * @var bool
     */
    public $incrementing = true;

    /**
     * 主鍵資料型態
     *
     * @var string
     */
    protected $keyType = 'int';

    /**
     * 建立或更新時，是否自動設定created_at、updated_at欄位
     *
     * @var bool
     */
    public $timestamps = true;

    /**
     * 自訂時戳的格式
     *
     * @var string
     */
    protected $dateFormat = 'Y-m-d H:i:s';

    /**
     * 指定created_at欄位
     *
     * @var string|null
     */
    const CREATED_AT = 'created_at';

    /**
     * 指定updated_at欄位
     *
     * @var string|null
     */
    const UPDATED_AT = 'updated_at';
}
```