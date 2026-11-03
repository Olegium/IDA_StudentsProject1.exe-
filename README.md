# IDA_StudentsProject1.exe-

================================РЕШЕНИЕ1===================================

1) Вот наше задание 

<img width="490" height="276" alt="{3DDBA078-85A3-4EFA-9C7D-E94C6707F814}" src="https://github.com/user-attachments/assets/818cd6a3-60ec-4ea2-a620-d8e6d4235cf6" />

надо найти какой то ключ по поиску string не получили результатов печально придется думать

<img width="640" height="684" alt="{917519DB-6F3C-4CF4-9CC6-12412F5ABEB2}" src="https://github.com/user-attachments/assets/7cf68100-f228-4aca-ba70-4cd01c1ac1d9" />

тут у нас функция main есть это значит начало

<img width="793" height="222" alt="{0AED9936-13E1-4236-922B-2439F768A175}" src="https://github.com/user-attachments/assets/8f902ec3-4e4c-4e95-afb1-516104514d9b" />

в inmain ссылка только на функцию DialogFunc

<img width="675" height="1115" alt="{CE00C294-D290-4206-B51F-BDB1B7E590F9}" src="https://github.com/user-attachments/assets/06e51fdf-2d37-446d-b505-585434f78d02" />
<img width="523" height="472" alt="{1BC6CE69-143C-46D5-889E-BF1AF084F76D}" src="https://github.com/user-attachments/assets/4ca6ca30-a6b1-457c-9487-38ce4293ed0b" />

начинается самое интересное 

<img width="365" height="100" alt="{FDB292B7-CC58-45ED-8500-50D2D6020717}" src="https://github.com/user-attachments/assets/88e5a827-bd63-4e71-95c2-3b4cedc75472" />

ESP (Extended Stack Pointer) — указатель вершины стека (по факту непостоянный так как вершина стэка постоянно меняется указывает адресс памяти)

EBP — это временный указатель на определенную область стека (по факту постоянен указывает адресс памяти где переменная "не зависит от изменений данных стэка")

ИДЕЯ в том что ESP все стоят поочередно(это значит для них выделен кусок памяти целый который разбили на переменные)

получается 

  CHAR String[5]; // [esp+60h] [ebp-208h] BYREF 
  +
  _BYTE v17[4]; // [esp+65h] [ebp-203h] BYREF  
  +
  char v18; // [esp+69h] [ebp-1FFh]  
  +
  _BYTE v19[4]; // [esp+6Ah] [ebp-1FEh] BYREF 
  +
  char v20; // [esp+6Eh] [ebp-1FAh] 
  +
  _BYTE v21[501]; // [esp+6Fh] [ebp-1F9h] BYREF

В сумме дает что то цельное, то есть String + v17 + v18 + v19 + v20 + v21 = X

<img width="511" height="330" alt="{F9F72520-5316-482B-A0F5-0F2DFE626F81}" src="https://github.com/user-attachments/assets/8d84dd3f-b925-447f-b843-d145f6e04333" />

получаем что String[0-3] это буквы String[4] это дефис 

v7(v17) и v8(v21) и v13(v19) переводятся в числа и сравниваются v7+v8=v13 иначе плохо

v18 и v20 это дефис -

получается String(буквы)+String(-)+v17(цифры)+v18(дефис)+v19(цифры)+v20(дефис)+v21(цифры)=x

<img width="956" height="457" alt="{F7245157-D9F1-405C-ACE8-EFDE1440D4A4}" src="https://github.com/user-attachments/assets/4c46bca4-7d11-4cac-a074-2c467d86f113" />

считаем по памяти длинну переменных и вот получаем 

ответ

<img width="474" height="263" alt="{6C083D75-3CA8-4754-80E2-A67BC23C21D2}" src="https://github.com/user-attachments/assets/d7f29e6f-b60d-4339-b21a-21cc3581972e" />

Наслаждаемся цветением сакуры

========================РЕШЕНИЕ2=================================

Убираем все проверки на ввод

cmp eax, ebx    ; вычисляет eax - ebx, флаги по результату ZF=1 если eax == ebx

test a, b       ; вычисляет (a AND b), результат выбрасывает, ставит флаги ZF = 1 если a AND b == 0 (нет общих единичных битов)

jz метка      ; Jump if Zero → прыгает, если ZF = 1

jnz метка     ; Jump if Not Zero → прыгает, если ZF = 0

заменяем с patch program patch the bytes все биты на 90... и получаем nop( это пустота )

   Было: 0F 85 78 01 00 00
   
   Стало: 90 90 90 90 90 90

<img width="479" height="1103" alt="{F9705E92-CCC3-4B71-8F82-54A4CD623658}" src="https://github.com/user-attachments/assets/f021a8af-e254-43cf-87d7-1e453d5b2531" />


<img width="652" height="1123" alt="{BEF8914C-2790-4D81-B519-42131BA18902}" src="https://github.com/user-attachments/assets/af94d3ab-6ffd-416b-9de7-486c060e0289" />

<img width="512" height="271" alt="{4AF2CD82-C7F1-482D-BCAC-1ACF516F76F4}" src="https://github.com/user-attachments/assets/64e99308-7d9f-493f-bb07-071f21e94e3e" />
