### Грамотное разбиение диска с LVM

| Раздел | Точка монтирования | Файловая система | Размер | Назначение |
| ------- | ----------- | ------- | ------- | ------- |
| `/boot` | /boot/efi | FAT32 | 1 ГБ | Загрузчик |
| `/(root)` | / | ext4 | 50–100 ГБ | Система и программы |
| `/home` | /home | ext4 | Оставшееся | Пользовательские файлы |
| `/var` | /var | ext4 | ~ | Логи, кэш |
| `/srv` | /srv | ext4 | ~ | Файлы сервисов | |
| `/tmp` | /tmp | ext4 | ~ | Временные файлы |
| `/swap` | - | swap | =RAM или +50% | Файл подкачки |

![image](https://github.com/user-attachments/assets/334971fa-5513-4b20-b9d2-fbe169098658)


![image](https://github.com/user-attachments/assets/03e8134c-5ad3-451c-9854-35335279f72b)
![image](https://github.com/user-attachments/assets/6e9432f1-cdc4-4aed-b4a8-0019cb25fe46)
![image](https://github.com/user-attachments/assets/7f8323f8-395c-442b-8902-b734a988af95)
![image](https://github.com/user-attachments/assets/8aead110-a90c-44ed-b508-3b560a8ad182)
![image](https://github.com/user-attachments/assets/d54e0eb1-2219-4925-9a6c-dc618654d6e3)
![image](https://github.com/user-attachments/assets/223ecfe8-2c5c-443d-8a0c-f0ae06927b82)
![image](https://github.com/user-attachments/assets/5d31ab6b-8e50-4342-989b-d7ea245ede95)
![image](https://github.com/user-attachments/assets/344f0b3c-1b4f-44c3-a4a2-e44caa1ea6a7)
![image](https://github.com/user-attachments/assets/17426106-01d3-4216-9c79-491ad3f854a7)
![image](https://github.com/user-attachments/assets/98ce9820-f226-47a0-9c99-452d2218a7be)
![image](https://github.com/user-attachments/assets/db9aaf5f-1b0c-4cf4-abfc-f0631955d621)
![image](https://github.com/user-attachments/assets/3b4ee655-a2cc-47bc-b99d-bb9d0df24851)
![image](https://github.com/user-attachments/assets/0dd70322-21ff-41ff-b732-559045da4c9e)
![image](https://github.com/user-attachments/assets/d33ef0c9-cf62-4a7e-8da7-82320168670f)
![image](https://github.com/user-attachments/assets/203e1fa4-25df-480c-b7bb-2fbbb1b18f3b)
![image](https://github.com/user-attachments/assets/90a5bc67-a838-4255-b15a-ff38ec4d9d62)
![image](https://github.com/user-attachments/assets/25c1ede4-14fe-481c-9490-f948acac2f06)
![image](https://github.com/user-attachments/assets/3ec6612b-fbaf-45a2-86c1-33bfc177c15d)
![image](https://github.com/user-attachments/assets/fe586345-972a-413a-892b-ff600fcb54e7)
![image](https://github.com/user-attachments/assets/a72becec-9ff7-4487-96b2-3cb024da8f2f)
![image](https://github.com/user-attachments/assets/df61e803-5e11-40c7-83e8-a1838ac7daf7)
![image](https://github.com/user-attachments/assets/25fa1580-1967-42c7-ab47-0ff15eb82b40)
![image](https://github.com/user-attachments/assets/1c82b6cd-58f5-48fe-bae7-8d0b7d2037d2)
![image](https://github.com/user-attachments/assets/45acd10e-ae22-4bdb-8807-b4da78b7a9ae)
![image](https://github.com/user-attachments/assets/733615b4-1573-477b-8a0e-d112cf89e56a)
![image](https://github.com/user-attachments/assets/7cfd8f43-2e5f-4f20-9ae8-5f1fb1aef322)
![image](https://github.com/user-attachments/assets/8f75e467-6b57-4f01-aa74-f8cf3c6eef3f)
![image](https://github.com/user-attachments/assets/c71baa65-4b6c-403d-89e0-5ce03c77ceb0)
![image](https://github.com/user-attachments/assets/28a0dac1-9946-41d5-b35a-ca3d634261b4)
![image](https://github.com/user-attachments/assets/47b6d061-9845-4f5c-8d17-930c839a7c53)
![image](https://github.com/user-attachments/assets/1d6f0a81-3a57-44e7-a312-c813f3b85c34)
![image](https://github.com/user-attachments/assets/3aee35aa-5f53-470b-888e-d0b93a6076b4)
![image](https://github.com/user-attachments/assets/658aadb0-e1cd-4006-ba04-357ac4e03be3)
![image](https://github.com/user-attachments/assets/8e588a57-bff6-4f24-86e1-3bf117b5643b)
![image](https://github.com/user-attachments/assets/83e428ab-e720-4bd9-9a82-4e917a24f5d2)
![image](https://github.com/user-attachments/assets/b36659b7-4aaf-47a1-9230-5d0969b14a97)


