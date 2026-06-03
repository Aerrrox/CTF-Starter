# 🛠️ Шпаргалка по инструментам CTF

Быстрый справочник — какой инструмент использовать в какой ситуации.

---

## Универсальные онлайн-инструменты

| Инструмент | Назначение | Ссылка |
|-----------|-----------|--------|
| CyberChef | Декодирование, шифры, анализ данных | https://gchq.github.io/CyberChef/ |
| dcode.fr | Определение и взлом классических шифров | https://www.dcode.fr/ |
| CrackStation | Взлом хэшей по словарю | https://crackstation.net/ |
| HackTricks | Огромная база техник и чеклистов | https://book.hacktricks.xyz/ |

---

## Crypto

```bash
# Определить тип хэша
hash-identifier <hash>

# Взлом MD5/SHA1 через словарь
hashcat -m 0 hash.txt wordlist.txt
john --format=raw-md5 hash.txt

# Работа с RSA (если есть n, e, c)
# Использовать RsaCtfTool
python3 RsaCtfTool.py --publickey key.pem --uncipherfile encrypted.txt
```

---

## Forensics

```bash
# Определить тип файла
file suspicious_file

# Извлечь строки из бинарного файла
strings file.bin

# HEX-дамп
xxd file.bin | head -50

# Метаданные изображения
exiftool image.jpg

# Анализ файловой системы внутри файла
binwalk -e archive.bin
```

---

## Steganography

```bash
# Скрытые данные в изображении
steghide extract -sf image.jpg

# LSB стеганография
zsteg image.png

# Анализ PNG чанков
pngcheck image.png

# Аудио-стеганография — открой в Audacity и посмотри спектрограмму
```

---

## Web

```bash
# Просмотр заголовков HTTP
curl -I https://target.com

# Базовый SQL injection тест
' OR 1=1--
" OR "1"="1

# Поиск скрытых директорий
gobuster dir -u http://target.com -w /usr/share/wordlists/dirb/common.txt

# Просмотр cookies в браузере
# DevTools (F12) → Application → Cookies
```

---

## OSINT

```bash
# Google dorks
site:target.com filetype:pdf
"target" inurl:admin
intitle:"index of" target

# Поиск по IP
whois 1.2.3.4
nmap -sV 1.2.3.4

# Поиск по email / username
# https://whatsmyname.app/
# https://hunter.io/
```

---

## Полезные команды Linux для CTF

```bash
# Поиск файлов
find / -name "flag*" 2>/dev/null
find / -perm -4000 2>/dev/null  # SUID файлы

# Декодирование Base64
echo "SGVsbG8=" | base64 -d

# XOR двух файлов
python3 -c "
a = open('file1','rb').read()
b = open('file2','rb').read()
print(bytes(x^y for x,y in zip(a,b)))"

# Перебор ZIP-пароля
fcrackzip -u -D -p /usr/share/wordlists/rockyou.txt archive.zip
```

---

*Нет нужного инструмента? Предложи добавить через [Issue](../../issues)!*
