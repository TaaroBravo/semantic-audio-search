FROM python:3.11-slim

RUN apt-get update && apt-get install -y \
    ffmpeg git build-essential libsndfile1 wget \
 && rm -rf /var/lib/apt/lists/*

ENV PANN_DIR=/app/panns

WORKDIR /app
COPY requirements.txt /app/requirements.txt
RUN pip install --upgrade pip && \
    pip install --no-cache-dir -r /app/requirements.txt

RUN mkdir -p ${PANN_DIR} && \
    wget -q -O ${PANN_DIR}/Cnn14_mAP=0.431.pth "https://zenodo.org/record/3987831/files/Cnn14_mAP%3D0.431.pth?download=1" && \
    wget -q -O ${PANN_DIR}/class_labels_indices.csv "https://raw.githubusercontent.com/qiuqiangkong/audioset_tagging_cnn/master/metadata/class_labels_indices.csv"

COPY main.py /app/main.py
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
