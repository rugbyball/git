##0. account_deals$add(新增帐户交易记录 (外部交易))
### arguments

|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|account_id|帐户编号|integer|NULL::integer|IN|
|payment_id|支付方式编号|integer|NULL::integer|IN|
|finance_center_id|金融中心编号|integer|NULL::integer|IN|
|account_deal_type|交易类型 (1，存入；2，提现) 提现金额前加负号|integer|NULL::integer|IN|
|amount|交易金额|numeric|0.0|IN|
|currency_id|货币编号|integer|NULL::integer|IN|
|note|註记|character varying|NULL::character varying|IN|
|paid_time|付款日期|timestamp with time zone|now()|IN|
|admin_ip|管理员IP|character varying|NULL::character varying|IN|
|admin_account_id|管理员编号|integer|NULL::integer|IN|
|admin_note|管理员註记|character varying|NULL::character varying|IN|

### samples
```
SELECT droi_ecommerce."account_deals$add"(account_id => 1,
                            payment_id => 3,
                            finance_center_id => 1,
                            account_deal_type => 1,
                            amount => 20000,
                            currency_id => 1,
                            note => '金融中心活动充值',
                            paid_time => now(), admin_ip => null,
                            admin_account_id => 9,
                            admin_note => null); 

```
[account_deals$add.sql](tests/functions/account_deals$add.sql)
##1. accounts$add(新增帐户)
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|finance_center_id|金融中心编号|integer|NULL::integer|IN|
|account_type|帐户类型 (1，管理帐户；2，活动帐户；3，一般帐户)。一般帐户只可对本人应用用户充值；管理帐户才可对非本人应用用户充值|integer|3|IN|
|name|帐户名称|character varying|NULL::character varying|IN|
|description|帐户描述|character varying|NULL::character varying|IN|
|account_balance|帐户余额|numeric|0.0|IN|
|visit_count|访问次数|integer|0|IN|
|is_validated|是否已验证|boolean|false|IN|

### samples
```
SELECT droi_ecommerce."accounts$add"(finance_center_id => 1,
                                account_type => 2,
                                name => '金融中心业务帐户',
                                description => '',
                                account_balance => 0.0,
                                visit_count => 0,
                                is_validated => True);

```
[accounts$add.sql](tests/functions/accounts$add.sql)
##2. account_users$add(新增帐户用户绑定)
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|app_id|应用编号|integer|NULL::integer|IN|
|account_id|帐户编号|integer|NULL::integer|IN|
|user_id|用户编号|integer|NULL::integer|IN|

### samples
```
SELECT droi_ecommerce."account_users$add"(app_id => 2,account_id => 5, user_id => 1);

```
[account_users$add.sql](tests/functions/account_users$add.sql)
##3. apps$add(新增应用)
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|finance_center_id|金融中心编号|integer|NULL::integer|IN|
|transfer_enabled|是否启用转帐|boolean|false|IN|
|cross_app_transfer_enabled|是否启用跨應用转帐 (TRUE，启用；FALSE，停用) 只可同帐户下用户互转|boolean|false|IN|
|name|应用名称|character varying|''::character varying|IN|
|brief|应用简介|character varying|NULL::character varying|IN|
|description|应用描述|character varying|NULL::character varying|IN|
|keywords|应用关键词|character varying|NULL::character varying|IN|

### samples
```
SELECT droi_ecommerce."apps$add"(finance_center_id => 1,
                                transfer_enabled => False,
                                cross_app_transfer_enabled => False, 
                                name => '卓易市场',
                                brief => '卓易市场APP',
                                description => null,
                                keywords => null);

```
[apps$add.sql](tests/functions/apps$add.sql)
##4. categories$add(新增商品分类)
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|app_id|应用编号|integer|NULL::integer|IN|
|name|分类名称|character varying|NULL::character varying|IN|
|brief|分类简介|character varying|NULL::character varying|IN|
|description|分类描述|character varying|NULL::character varying|IN|
|keywords|分类关键词|character varying|NULL::character varying|IN|
|parent_id|上级分类|integer|NULL::integer|IN|
|sort_order|排序序号|integer|NULL::integer|IN|
|measure_unit|数量单位|character varying|NULL::character varying|IN|
|is_visible|是否显示|boolean|false|IN|

### samples
```
SELECT droi_ecommerce."categories$add"(app_id => 5,
                                name => '每天听本书',
                                brief => null,
                                description => null,
                                keywords => null,
                                parent_id => null,
                                sort_order => 1,
                                measure_unit => '本',
                                is_visible => True);

```
[categories$add.sql](tests/functions/categories$add.sql)
##5. cross_app_user_transfer_maps$add(新增跨应用用户转帐对应)
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|from_app_id|来源应用编号|integer|NULL::integer|IN|
|to_app_id|标的应用编号|integer|NULL::integer|IN|

### samples
```
SELECT droi_ecommerce."cross_app_user_transfer_maps$add"(from_app_id => 2, to_app_id => 3);
```
[cross_app_user_transfer_maps$add.sql](tests/functions/cross_app_user_transfer_maps$add.sql)
##6. currencies$add(新增货币)
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|finance_center_id|金融中心编号|integer|NULL::integer|IN|
|app_id|应用编号|integer|NULL::integer|IN|
|currency_type|货币类型 (1，结算货币；2，App兑换货币；3，App专属货币)|integer|3|IN|
|code|货币代号|character varying|NULL::character varying|IN|
|name|货币名称|character varying|''::character varying|IN|
|is_enabled|是否启用|boolean|false|IN|

### samples
```
SELECT droi_ecommerce."currencies$add"(finance_center_id => 1,
                                app_id => null,
                                currency_type => 1,
                                code => 'DRB',
                                name => '卓易币',
                                is_enabled => True);

```
[currencies$add.sql](tests/functions/currencies$add.sql)
##7. exrates$add(新增汇率 (只可新增、修改，不可删除))
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|finance_center_id|金融中心编号|integer|NULL::integer|IN|
|currency_id|货币编号|integer|NULL::integer|IN|
|base_currency_id|基础货币编号|integer|NULL::integer|IN|
|exrate|汇率，修改时只可改此栏位|numeric|1.0|IN|
|is_enabled|是否启用|boolean|false|IN|

### samples
```
SELECT droi_ecommerce."exrates$add"(finance_center_id => 1,
                                currency_id => 2,
                                base_currency_id => 1,
                                exrate => 10000,
                                is_enabled => True);

```
[exrates$add.sql](tests/functions/exrates$add.sql)
##8. finance_centers$add(新增金融中心)
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|transfer_enabled|是否启用转帐|boolean|false|IN|
|name|购物中心名称|character varying|''::character varying|IN|
|brief|购物中心简介|character varying|NULL::character varying|IN|
|description|购物中心描述|character varying|NULL::character varying|IN|
|keywords|购物中心关键词|character varying|NULL::character varying|IN|

### samples
```
SELECT droi_ecommerce."finance_centers$add"(transfer_enabled => TRUE,
						name => '卓易金融中心',
						brief => '卓易',
						description => '卓易',
						keywords => '卓易,金融');
```
[finance_centers$add.sql](tests/functions/finance_centers$add.sql)
##9. payments$add(新增支付方式)
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|finance_center_id|金融中心编号|integer|NULL::integer|IN|
|code|支付代号|character varying|''::character varying|IN|
|name|支付名称|character varying|''::character varying|IN|
|description|支付描述|character varying|NULL::character varying|IN|
|is_enabled|是否启用|boolean|false|IN|

### samples
```
SELECT droi_ecommerce."payments$add"(finance_center_id => 1,
                                code => 'alipay',
                                name => '支付宝',
                                description => '支付宝网站(www.alipay.com) 是国内先进的网上支付平台',
                                is_enabled => True);

```
[payments$add.sql](tests/functions/payments$add.sql)
##10. products$add(新增商品)
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|app_id|应用编号|integer|NULL::integer|IN|
|category_id|分类编号|integer|NULL::integer|IN|
|barcode|商品条码|character varying|NULL::character varying|IN|
|name|商品名称|character varying|NULL::character varying|IN|
|brief|商品简介|character varying|NULL::character varying|IN|
|description|商品描述|character varying|NULL::character varying|IN|
|keywords|商品关键词|character varying|NULL::character varying|IN|
|seller_note|卖家说明|character varying|NULL::character varying|IN|
|cat_id1|分类编号1|integer|NULL::integer|IN|
|cat_id2|分类编号2|integer|NULL::integer|IN|
|cat_id3|分类编号3|integer|NULL::integer|IN|
|cat_id4|分类编号4|integer|NULL::integer|IN|
|cat_id5|分类编号5|integer|NULL::integer|IN|
|brand_id|品牌编号|integer|NULL::integer|IN|
|is_real|是否为实体商品|boolean|false|IN|
|product_status|商品状态 (1，上架；2，下架)|integer|2|IN|
|inventory_amount|商品库存量|integer|0|IN|
|inventory_warn_amount|商品库存告警存量|integer|0|IN|
|volume|商品体积|numeric|0.0|IN|
|weight|商品重量|numeric|0.0|IN|
|can_alone_sale|可单独销售|boolean|true|IN|
|currency_id|货币编号|integer|NULL::integer|IN|
|purchase_price|进货价格|numeric|NULL::numeric|IN|
|market_price|市场价格|numeric|NULL::numeric|IN|
|app_price|本店售价|numeric|NULL::numeric|IN|
|promote_id|促销编号|integer|NULL::integer|IN|
|promote_price|促销价格|numeric|NULL::numeric|IN|
|promote_start_time|促销起日|timestamp with time zone|NULL::timestamp with time zone|IN|
|promote_end_time|促销迄日|timestamp with time zone|NULL::timestamp with time zone|IN|
|member_price|会员价格|numeric|NULL::numeric|IN|
|shipping_costs|商品运费|numeric|NULL::numeric|IN|
|shipping_type_id|配送方式编号|integer|NULL::integer|IN|
|is_cod|是否支持货到付款|boolean|false|IN|
|click_count|商品点击数|integer|0|IN|
|is_promote|促销商品|boolean|false|IN|
|is_recommend|推荐商品|boolean|false|IN|
|is_new|新品|boolean|false|IN|
|is_hot|热销|boolean|false|IN|
|sort_order|商品排序|integer|1|IN|
|is_delete|是否已删除|boolean|false|IN|

### samples
```
SELECT droi_ecommerce."products$add"(app_id => 5,
                                category_id => 4,
                                barcode => null,
                                name => '通往财富自由之路',
                                brief => '专栏订阅1',
                                description => null,
                                keywords => null,
                                seller_note => null,
                                cat_id1 => null,
                                cat_id2 => null,
                                cat_id3 => null,
                                cat_id4 => null,
                                cat_id5 => null,
                                brand_id => null,
                                is_real => False,
                                product_status => 1,
                                inventory_amount => 9999999,
                                inventory_warn_amount => 10,
                                volume => null,
                                weight => null,
                                can_alone_sale => True,
                                purchase_price => null,
                                market_price => null,
                                app_price => 199,
                                promote_id => null,
                                promote_price => null,
                                promote_start_time => null,
                                promote_end_time => null,
                                member_price => null,
                                shipping_costs => null,
                                shipping_type_id => null,
                                is_cod => null,
                                click_count => null,
                                is_promote => False,
                                is_recommend => False,
                                is_new => False,
                                is_hot => False,
                                sort_order => 1,
                                is_delete => False,
                                currency_id => 7);

```
[products$add.sql](tests/functions/products$add.sql)
##11. promotes$add(新增促销)
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|app_id|应用编号|integer|NULL::integer|IN|
|product_id|商品编号|integer|NULL::integer|IN|
|promote_type|促销类型 (1，赠品；2，现金减免；3，价格折扣)|integer|NULL::integer|IN|
|promote_type_ext|促销类型参数|character varying|NULL::character varying|IN|
|app_price|原价|numeric|0.0|IN|
|promote_price|促销价|numeric|0.0|IN|
|currency_id|货币编号|integer|NULL::integer|IN|
|start_time|促销起日|timestamp with time zone|NULL::timestamp with time zone|IN|
|end_time|促销迄日|timestamp with time zone|NULL::timestamp with time zone|IN|

### samples
```
SELECT droi_ecommerce."promotes$add"(app_id => 5,
                                product_id => 6,
                                promote_type => 2,
                                promote_type_ext => '8.01',
                                promote_price => 9.99,
                                start_time => '2016-09-14 00:00:00',
                                end_time => '2016-09-15 00:00:00',
                                app_price => 18,
                                currency_id => 2);

```
[promotes$add.sql](tests/functions/promotes$add.sql)
##12. shipping_types$add(新增配送类型)
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|app_id|应用编号|integer|NULL::integer|IN|
|code|配送代号|character varying|NULL::character varying|IN|
|name|配送名称|character varying|NULL::character varying|IN|
|description|配送描述|character varying|NULL::character varying|IN|
|insure|保价费用|numeric|0.0|IN|
|support_cod|是否支持货到付款|boolean|false|IN|
|is_enabled|配送方式是否可用|boolean|false|IN|
|shipping_print|未定义1|character varying|NULL::character varying|IN|
|print_bg|未定义2|character varying|NULL::character varying|IN|
|config_label|未定义3|character varying|NULL::character varying|IN|
|print_model|未定义4|character varying|NULL::character varying|IN|
|shipping_order|未定义5|integer|NULL::integer|IN|

### samples
```
SELECT droi_ecommerce."shipping_types$add"(app_id => 5,
                                    code => 'vp',
                                    name => '虚拟商品',
                                    description => '虚拟商品不需配送',
                                    insure => 0,
                                    support_cod => False,
                                    is_enabled => True,
                                    shipping_print => null,
                                    print_bg => null,
                                    config_label => null,
                                    print_model => '0',
                                    shipping_order => 0);

```
[shipping_types$add.sql](tests/functions/shipping_types$add.sql)
##13. user_deals$add(新增用户交易记录 (内部交易))
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|user_id|用户编号|integer|NULL::integer|IN|
|user_deal_type|交易类型 (1，存入；2，提现)|integer|NULL::integer|IN|
|amount|交易金额|numeric|0.0|IN|
|currency_id|货币编号|integer|NULL::integer|IN|
|note|註记|character varying|NULL::character varying|IN|

##14. users$add(新增用户)
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|app_id|应用编号|integer|NULL::integer|IN|
|user_type|帐户类型 (1，管理用户；2，活动用户；3，一般用户)|integer|3|IN|
|user_rank|用户等级|integer|NULL::integer|IN|
|name|用户名称|character varying|NULL::character varying|IN|
|visit_count|访问次数|integer|0|IN|
|is_validated|是否已验证 (TRUE，已验证；FALSE，尚未验证)|boolean|false|IN|

### samples
```
SELECT droi_ecommerce."users$add"(app_id => 2,
                            user_type => 3,
                            user_rank => null,
                            name => 'owen_夺宝',
                            visit_count => 0,
                            is_validated => False);

```
[users$add.sql](tests/functions/users$add.sql)
##15. account_user_logs$get(查询帐户用户交易记录)
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|q_account_user_log_id|帐户用户交易记录编号|integer|NULL::integer|IN|
|finance_center_id|金融中心编号|integer|None|OUT|
|account_id|帐户编号|integer|None|OUT|
|user_id|用户编号|integer|None|OUT|
|user_deal_id|用户交易记录|integer|None|OUT|
|exchange_log_id|换汇记录编号|integer|None|OUT|
|fc_currency_id|金融中心货币编号|integer|None|OUT|
|fc_amount|金融中心货币金额 (若由用户提现，前加负号)|numeric|None|OUT|
|note|註记|character varying|None|OUT|
|create_time|建立日期|timestamp with time zone|None|OUT|
|account_user_id|帐户用户绑定编号|integer|None|OUT|
|app_id|应用编号|integer|None|OUT|
|account_deal_id|帐户交易记录编号|integer|None|OUT|
|app_currency_id|用户应用中货币编号|integer|None|OUT|
|app_amount|用户应用中货币金额 (若由用户提现，前加负号)|numeric|None|OUT|

##16. account_users$get(查询帐户用户绑定)
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|q_user_id|用户编号|integer|NULL::integer|IN|
|q_account_id|帐户编号|integer|NULL::integer|IN|
|account_user_id|帐户用户绑定编号|integer|None|OUT|
|q_app_id|应用编号|integer|NULL::integer|IN|
|account_user_id|帐户用户绑定编号|integer|None|OUT|
|account_id|帐户编号|integer|None|OUT|
|app_id|应用编号|integer|None|OUT|
|account_id|帐户编号|integer|None|OUT|
|user_id|用户编号|integer|None|OUT|
|app_id|应用编号|integer|None|OUT|
|user_id|用户编号|integer|None|OUT|

##17. account_users$get(查询帐户用户绑定)
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|q_user_id|用户编号|integer|NULL::integer|IN|
|q_account_id|帐户编号|integer|NULL::integer|IN|
|account_user_id|帐户用户绑定编号|integer|None|OUT|
|q_app_id|应用编号|integer|NULL::integer|IN|
|account_user_id|帐户用户绑定编号|integer|None|OUT|
|account_id|帐户编号|integer|None|OUT|
|app_id|应用编号|integer|None|OUT|
|account_id|帐户编号|integer|None|OUT|
|user_id|用户编号|integer|None|OUT|
|app_id|应用编号|integer|None|OUT|
|user_id|用户编号|integer|None|OUT|

##18. app_currencies$getall()
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|q_finance_center_id|金融中心编号|integer|NULL::integer|IN|
|q_app_id|应用编号|integer|NULL::integer|IN|
|currency_id|货币编号|integer|None|OUT|
|code|货币代号|character varying|None|OUT|
|name|货币名称|character varying|None|OUT|

##19. exrates$get(查询汇率 (只可新增、修改，不可删除))
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|q_finance_center_id|金融中心编号|integer|NULL::integer|IN|
|q_currency_id|货币编号|integer|NULL::integer|IN|
|q_base_currency_id|基础货币编号|integer|NULL::integer|IN|
|exrate_id|汇率编号|integer|None|OUT|
|exrate|汇率，修改时只可改此栏位|numeric|None|OUT|

##20. finance_center_currencies$get()
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|q_finance_center_id|金融中心编号|integer|NULL::integer|IN|
|currency_id|货币编号|integer|None|OUT|
|code|货币代号|character varying|None|OUT|
|name|货币名称|character varying|None|OUT|

##21. account_deposit()
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|account_id||integer|NULL::integer|IN|
|payment_id||integer|NULL::integer|IN|
|finance_center_id||integer|NULL::integer|IN|
|amount||numeric|0.0|IN|
|currency_id||integer|NULL::integer|IN|
|note||character varying|NULL::character varying|IN|
|paid_time||timestamp with time zone|now()|IN|
|admin_ip||character varying|NULL::character varying|IN|
|admin_account_id||integer|NULL::integer|IN|
|admin_note||character varying|NULL::character varying|IN|

##22. account_transfer()
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|from_account_id||integer|NULL::integer|IN|
|to_account_id||integer|NULL::integer|IN|
|finance_center_id||integer|NULL::integer|IN|
|amount||numeric|0.0|IN|
|currency_id||integer|NULL::integer|IN|
|note||character varying|NULL::character varying|IN|
|admin_ip||character varying|NULL::character varying|IN|
|admin_account_id||integer|NULL::integer|IN|
|admin_note||character varying|NULL::character varying|IN|

##23. account_user_transfer()
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|finance_center_id||integer|NULL::integer|IN|
|from_account_id||integer|NULL::integer|IN|
|from_amount||numeric|0.0|IN|
|to_app_id||integer|NULL::integer|IN|
|to_app_currency_id||integer|NULL::integer|IN|
|to_user_id||integer|NULL::integer|IN|
|note||character varying|NULL::character varying|IN|
|admin_ip||character varying|NULL::character varying|IN|
|admin_account_id||integer|NULL::integer|IN|
|admin_note||character varying|NULL::character varying|IN|

##24. cross_app_user_transfers()
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|finance_center_id||integer|NULL::integer|IN|
|from_app_id||integer|NULL::integer|IN|
|to_app_id||integer|NULL::integer|IN|
|from_user_id||integer|NULL::integer|IN|
|to_user_id||integer|NULL::integer|IN|
|from_currency_id||integer|NULL::integer|IN|
|to_currency_id||integer|NULL::integer|IN|
|from_amount||numeric|0.0|IN|
|note||character varying|NULL::character varying|IN|
|admin_ip||character varying|NULL::character varying|IN|
|admin_account_id||integer|NULL::integer|IN|
|admin_note||character varying|NULL::character varying|IN|

##25. is_account_transfer_enabled()
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|finance_center_id||integer|NULL::integer|IN|

##26. is_cross_app_user_transfer_enabled()
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|app_id||integer|NULL::integer|IN|

##27. is_currency_enabled()
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|currency_id||integer|NULL::integer|IN|

##28. is_user_transfer_enabled()
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|app_id||integer|NULL::integer|IN|

##29. raise_exception_if_not_true()
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|check_boolean||boolean|false|IN|
|exception_msg||character varying|NULL::character varying|IN|

##30. user_account_transfer()
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|finance_center_id||integer|NULL::integer|IN|
|from_app_id||integer|NULL::integer|IN|
|from_app_currency_id||integer|NULL::integer|IN|
|from_user_id||integer|NULL::integer|IN|
|from_amount||numeric|0.0|IN|
|to_account_id||integer|NULL::integer|IN|
|note||character varying|NULL::character varying|IN|
|admin_ip||character varying|NULL::character varying|IN|
|admin_account_id||integer|NULL::integer|IN|
|admin_note||character varying|NULL::character varying|IN|

##31. user_transfer()
### arguments
|parameter_name|parameter_name_cn|data_type|parameter_default|parameter_mode|
|-------|-------|-------|-------|
|from_user_id||integer|NULL::integer|IN|
|to_user_id||integer|NULL::integer|IN|
|currency_id||integer|NULL::integer|IN|
|amount||numeric|0.0|IN|
|note||character varying|NULL::character varying|IN|

