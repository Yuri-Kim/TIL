## GPU사용하기  

Tensorflow의 계산 과정이 CPU와 GPU를 모두 지원한다면 GPU 우선 배치 (ex. matmul)  
어떤 디바이스에 연산/Tensor가 배치되었는지 확인  

    sess = tf.Session(config=tf.ConfigProto(log_device_placement=True))  

탄력적으로 GPU memory 사용  

    config = tf.ConfigProto()  
    config.gpu_options.allow_growth = True   
    session = tf.Session(config=config, ...)  


<!--stackedit_data:
eyJoaXN0b3J5IjpbODQzODU0Nzg0XX0=
-->