# PHP 以太坊 BSC链 接口 SDK 区块链接口 币安智能链
## 1：创建钱包地址
## 2: 还原助记词
## 3：主币转账
## 4：代币转账
## 5：主币查询余额
## 6：代币查询余额
## 7：监控代币合约的转账事件
## 8：监控主币的transfer事件
## 9：授权【服务端授权】
## 10 授权转出代币
## 11：监控授权的记录，监控合约

# 调用的php代码如下
~~~
<?php
require_once './eth.class.php';
$eth = new Eth() ;
$from = 'xxxxxxxxxx';//from 地址 
$private_key = "私钥";

$to = "xxxxxxxxxxxxxxxxxxxxxxx";

$contract = '0x8EbCcd8a2B54b44f911ce942ddF35a560cbbDdD6';//测试的

$contract = '0x55d398326f99059ff775485246999027b3197955';//线上的

$abi = '[{"constant":true,"inputs":[],"name":"mintingFinished","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"name","outputs":[{"name":"","type":"string"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"_spender","type":"address"},{"name":"_value","type":"uint256"}],"name":"approve","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"totalSupply","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"_from","type":"address"},{"name":"_to","type":"address"},{"name":"_value","type":"uint256"}],"name":"transferFrom","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"decimals","outputs":[{"name":"","type":"uint8"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"unpause","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":false,"inputs":[{"name":"_to","type":"address"},{"name":"_amount","type":"uint256"}],"name":"mint","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"paused","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"_spender","type":"address"},{"name":"_subtractedValue","type":"uint256"}],"name":"decreaseApproval","outputs":[{"name":"success","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"_owner","type":"address"}],"name":"balanceOf","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"pause","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"owner","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"symbol","outputs":[{"name":"","type":"string"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"_to","type":"address"},{"name":"_value","type":"uint256"}],"name":"transfer","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"mintTotal","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"_spender","type":"address"},{"name":"_addedValue","type":"uint256"}],"name":"increaseApproval","outputs":[{"name":"success","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"_owner","type":"address"},{"name":"_spender","type":"address"}],"name":"allowance","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"newOwner","type":"address"}],"name":"transferOwnership","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"inputs":[],"payable":false,"stateMutability":"nonpayable","type":"constructor"},{"payable":true,"stateMutability":"payable","type":"fallback"},{"anonymous":false,"inputs":[{"indexed":true,"name":"to","type":"address"},{"indexed":false,"name":"amount","type":"uint256"}],"name":"Mint","type":"event"},{"anonymous":false,"inputs":[],"name":"Pause","type":"event"},{"anonymous":false,"inputs":[],"name":"Unpause","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"previousOwner","type":"address"}],"name":"OwnershipRenounced","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"previousOwner","type":"address"},{"indexed":true,"name":"newOwner","type":"address"}],"name":"OwnershipTransferred","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"owner","type":"address"},{"indexed":true,"name":"spender","type":"address"},{"indexed":false,"name":"value","type":"uint256"}],"name":"Approval","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"from","type":"address"},{"indexed":true,"name":"to","type":"address"},{"indexed":false,"name":"value","type":"uint256"}],"name":"Transfer","type":"event"}]';

function createMnemonicWord(  ){
    global $eth ;
    $data  = $eth->createMnemonicWord(  );
    echo "助记词： $data \n";
}
//createMnemonicWord() ;



function generateAddress( $mnemonic = ''   ){
    global $eth ;
    $data  = $eth->generateAddress( $mnemonic  );
    echo "钱包地址:{$data['address']} \n私钥： {$data['private_key']} \n助记词：  {$data['mnemonic']}\n公钥：  {$data['public_key']}\n";
}

generateAddress() ;

function createAddress(  ){
    global $eth ;
    $data  = $eth->createAddress(  );
    echo "address:{$data['address']} , 私钥： {$data['private_key']}  \n";
}

//createAddress();

function privateKeyToAddress( $private_key ){
    global $eth ;
    $data  = $eth->privateKeyToAddress( $private_key );
    echo "address:{$data['address']} , 私钥： {$data['private_key']}  \n";
}

//privateKeyToAddress($private_key);


function get_balance( $address = '' ){
    global $eth ;
    $balance = $eth->get_balance($address );
    echo "address:{$address} , 主币余额：$balance \n";
}

//get_balance($from);




function trans($from , $to , $private_key , $amount , $remark =''){
    global $eth ;
    $txid = $eth->trans($from , $to , $private_key , $amount ,$remark );
    echo "主币转账成功， 交易id：$txid \n";
}
$amount = (string) 0.00028;

//trans($from , $to , $private_key , $amount , "trans交易" );


function getTransactionReceipt($txid = ''){
    global $eth ;
    $balance = $eth->getTransactionReceipt($txid );
    echo " \n";
}
//getTransactionReceipt("0xb9aff418a2015a9c50933b8a56ac0f8085a609a3e16d9dfdc46f5fa9ca1fb106");
//getTransactionReceipt("0xf979f0bf96da167adf55623c976470779fc8bf9bea6bc25e136d2c7ad3a92298");

function getTransactionByHash($txid = '' , $is_token = false ){
    global $eth ;
    $data  = $eth->getTransactionByHash($txid ,$is_token);
    echo "查询交易id：$txid 返回数据 \n";
    print_r($data);
    echo " \n";
}

//getTransactionByHash("0xb9aff418a2015a9c50933b8a56ac0f8085a609a3e16d9dfdc46f5fa9ca1fb106");
//getTransactionByHash("0xf979f0bf96da167adf55623c976470779fc8bf9bea6bc25e136d2c7ad3a92298" , true );



//代币转账
function token_trans($from , $to , $private_key , $amount , $contract , $abi ){
    global $eth ;
    try{
        $txid = $eth->token_trans($from , $to , $private_key , $amount , $contract , $abi );
        echo "代币转账成功， 交易id：$txid \n";

    }catch(\Exception $e ){
        echo "error : " . $e->getMessage();
    }
}

$amount = "0.59";
//token_trans($from , $to , $private_key , $amount , $contract , $abi ) ;

//代币余额
function token_balance($address , $contract , $abi ){
    global $eth ;
    try{
        $balance  = $eth->getTokenBalance($address , $contract , $abi );
        echo "address：{$address} 余额， {$balance} \n";
    }catch(\Exception $e ){
        echo "error : " . $e->getMessage();
    }
}
//token_balance($from  ,  $contract , $abi ) ;
//合约精度
function token_decimal($contract , $abi ){
    global $eth ;
    try{
        $balance  = $eth->token_decimal( $contract , $abi );
        echo "合约：{$contract} 精度， {$balance} \n";
    }catch(\Exception $e ){
        echo "error : " . $e->getMessage();
    }
}
//token_decimal( $contract , $abi ) ;

//合约授权额度
function getTokenAllowance($from , $to_address ,  $contract , $abi ){
    global $eth ;
    try{
        $balance  = $eth->getTokenAllowance($from ,$to_address ,  $contract , $abi );
        echo "钱包地址：{$from}  , 合约：{$contract} 授权额度， {$balance} \n";
    }catch(\Exception $e ){
        echo "error : " . $e->getMessage();
    }
}
//getTokenAllowance( $from , "0x68efb8e0dca3a6614351701d31b13032d9cb1829" , $contract , $abi ) ;


//代币授权
function token_approve($from , $to , $private_key , $amount , $contract , $abi ){
    global $eth ;
    try{
        $txid = $eth->token_approve($from , $to , $private_key , $amount , $contract , $abi );
        echo "代币授权成功， 交易id：$txid \n";

    }catch(\Exception $e ){
        echo "授权error : " . $e->getMessage();
    }
}

//$amount = "100";
//token_approve($from , $to , $private_key , $amount , $contract , $abi ) ;

//代币授权转出
function token_transfer_from($from , $to , $private_key , $amount , $contract , $abi ){
    global $eth ;
    try{
        $txid = $eth->token_transfer_from($from , $to , $private_key , $amount , $contract , $abi );
        echo "代币授权转出成功， 交易id：$txid \n";

    }catch(\Exception $e ){
        echo "授权转出error : " . $e->getMessage();
    }
}
//$amount = "1" ;
//token_transfer_from($from , 'xxxxxxxxxxx' , 'xxxxxxxx' , $amount , $contract , $abi ) ;

//主币的最新交易

function mainTrans(){
    global $eth ;
    while(1){
        try{
            $data = $eth->queryMainTrans();
            print_r($data);
            sleep(2);
        }catch(\Exception $e ){
            echo "error : " . $e->getMessage() . "\n";
        }
        echo "\n";
    }
}
//mainTrans();


//合约的最新交易
function queryContractTrans(){
    global $eth  , $contract  ;
    while(1){
        $data = $eth->queryContractTrans($contract );
        /*if(!empty($data)){
            $str = var_export($data , true ) ;
            file_put_contents("./trans.log" , $str . "\n"  , FILE_APPEND);
        }*/
        print_r($data);
        echo "success \n";
        sleep(2);
        echo "\n";
    }
}


//queryContractTrans();




//合约的授权交易
function queryContractApproveLog(){
    global $eth  , $contract  ;
    while(1){
        try{
            $data = $eth->queryContractApproveLog($contract , "xxxxxxxxxxxxxxxxxx");
            if(!empty($data)){
                // $str = var_export($data , true ) ;
                foreach ($data as $kk => $vv){
                    $str = "【" . date("Y-m-d H:i:s" , time() ) ."】";
                    $str .= json_encode($vv,JSON_UNESCAPED_UNICODE);
                    file_put_contents(  "./trans.log" , $str . "\n"  , FILE_APPEND);
                }
            }
            //print_r($data);
            echo  "【" . date("Y-m-d H:i:s" , time() ) ."】" . "success \n";
            sleep(2);
            echo "\n";
        }catch(\Exception $e ){
            echo  "【" . date("Y-m-d H:i:s" , time() ) ."】" . "error " . $e->getMessage() . "\n" ;
        }

    }
}


//queryContractApproveLog();



~~~