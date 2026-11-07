# ML_DLops 
Репозитарий для семинаров и домашних заданий по ML/DLops
# Семинар 1. Чтение данных из S3 (Inside Airbnb)

Ноутбук `01_read_data.ipynb` читает CSV из S3 (Yandex Object Storage) и при
недоступности S3 переключается на локальную копию `data/train.csv`.

## Окружение (conda)

```bash
conda create -n mlops26 python=3.11 -y
conda activate mlops26
conda install jupyterlab ipykernel pandas boto3 -y
python -m ipykernel install --user --name mlops26 --display-name "mlops26"
```

## Источник данных

- endpoint: `https://storage.yandexcloud.net`, region: `ru-central1`
- bucket: `mlops26-course-bucket`, key: `prepared/train.csv`
- URI: `s3://mlops26-course-bucket/prepared/train.csv`

Скачать локальную копию:

```bash
aws s3 cp s3://mlops26-course-bucket/prepared/train.csv data/train.csv \
    --endpoint-url https://storage.yandexcloud.net
```

Ключи доступа лежат в локальном `secretkeys.py` (`KEY_ID`, `ACCESS_KEY`),
файл в `.gitignore` и в репозиторий не попадает.

## Запуск ноутбука

Запускать **из корня репозитория**, иначе `data/train.csv` не найдётся:

```bash
conda activate mlops26
jupyter lab
```

Открыть `01_read_data.ipynb`, выбрать ядро **Python (mlops26)**, выполнять
ячейки сверху вниз. Перед коммитом: **Restart Kernel and Clear Outputs**,
затем сохранить — ноутбук уходит без выводов и без ключей.

## Примечания

- `data/`, `secretkeys.py`, `.ipynb_checkpoints/` — в `.gitignore`.
- Путь в коде: `'data/train.csv'` или `r'data\train.csv'`
  (без `r` строка `'data\train.csv'` содержит табуляцию `\t`).
