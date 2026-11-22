۱: ریاضیات در لینوکس

اسکریپتی بنویسید که یک عدد از کاربر دریافت کرده و زوج یا فرد بودن آن را مشخص کند.

کد (odd_even.sh)

#!/bin/bash

read -r -p "enter an integer: " NUM

if [[ ! "$NUM" =~ ^-?[0-9]+$ ]]; then
    echo "error: enter an integer."
    exit 1
fi

SIGN=""
if [[ "$NUM" == -* ]]; then
    SIGN="-"
    NUM="${NUM#-}"
fi

while [[ ${#NUM} -gt 1 && "$NUM" == 0* ]]; do
    NUM="${NUM#0}"
done

if (( NUM % 2 == 0 )); then
    echo "${SIGN}${NUM} is even."
else
    echo "${SIGN}${NUM}. Is odd ."
fi

Execution 

chmod +x odd_even.sh
./odd_even.sh

⸻

۲: تحلیل فایل‌ها

با ترکیب حلقه for و شرط if، اسکریپتی بنویسید که تمام فایل‌ها و دایرکتوری‌های موجود در دایرکتوری فعلی را با برچسب [FILE] برای فایل‌ها و [DIR] برای دایرکتوری‌ها چاپ کند.

کد (list_items.sh)

#!/bin/bash

shopt -s dotglob nullglob

for ITEM in *; do
    if [[ -f "$ITEM" ]]; then
        echo "[FILE] $ITEM"
    elif [[ -d "$ITEM" ]]; then
        echo "[DIR] $ITEM"
    fi
done

Execution 

chmod +x list_items.sh

./list_items.sh
