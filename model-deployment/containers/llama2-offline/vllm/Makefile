TENANCY:=${TENANCY_NAME}
CONTAINER_REGISTRY:=${REGION_KEY}.ocir.io

VLLM_INFERENCE_IMAGE:=${CONTAINER_REGISTRY}/${TENANCY}/vllm-odsc:1.0.0
VLLM_CONTAINER_NAME:=vllm-odsc

SOURCE_MODEL_DIR=/model
TARGET_MODEL_DIR=/opt/ds/model/deployed_model
TENSOR_PARALLELISM=2
PORT=8080

build:
	docker build -t ${VLLM_INFERENCE_IMAGE} -f Dockerfile .

push:
	docker push ${VLLM_INFERENCE_IMAGE}

run:
	docker run -e PORT=${PORT} -e MODEL=${TARGET_MODEL_DIR} -e TENSOR_PARALLELISM=${TENSOR_PARALLELISM} --shm-size=1gb -p ${PORT}:${PORT} -v ${SOURCE_MODEL_DIR}:${TARGET_MODEL_DIR}:Z -it --gpus all ${VLLM_INFERENCE_IMAGE}