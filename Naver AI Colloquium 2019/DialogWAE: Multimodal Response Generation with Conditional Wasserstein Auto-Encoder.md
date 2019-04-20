
## DialogWAE: Multimodal Response Generation with Conditional Wasserstein Auto-Encoder  

Presenter : Xiaodong Gu (NAVER)  

### Open-domain Dialogue Generation  
A : How are you?  
B : Good!  
A : How was the weather in your city?  
B : Good! How was the weather in your city?  
A : (next utterance)  

Hesitating among different ground truths → Favoring safe responses (e.g. "good", "I don't know")  

### DialogWAE - a GAN model to "generate" the latent variable  
 ![
](https://lh3.googleusercontent.com/HfeLH_MWLyFbl8in5eAj02Fs4bB2hDEuUvZ1Nu9n7j7KKIr3QkJuww1HmKNq_xmXTLVhJwaHV2rW "wae1")  

![enter image description here](https://lh3.googleusercontent.com/72bIXAD55WVlU4SwEG3HlkQjNBBuetMuptgLDpY8YULVTzPMk_DARXQwMEFTyo3N4wA6B9HcarVw "wae2")  

![
](https://lh3.googleusercontent.com/8DRjkU7K_WpnO-NNNyrJg3ykRHDYzOLOq9DG6vrEPlZXPMhzeoTCN-wmr1CI2pPXuu1lcyU0rooj "wae3")  

위 식에서  
Discriminator  
![
](https://lh3.googleusercontent.com/vwUgffrddexsBZn99c_ZZcSqIZGbU15SMqU6_wLoNawQNFz7I_uyKofb-o_ParU-FfWTQ80zr4ue "wae4")  
Generator   
![
](https://lh3.googleusercontent.com/SAl2omd5DtEBdAaBXGYWA3fsSzh5bXfqiz8UoWW2RMUggdTKtHb0Z8BLljDe4clozIu5qPsqJIiX "wae5")  

### DialogWAE  
![
](https://lh3.googleusercontent.com/tqCLS-5ygG2LPjLvT9Jcfr3lGkMr0R_k8ko0KHa1GeNAh9mjE_t5ooMthHiOIlqgFGCeaBOV3Xrb "wae6")  

Recogmition Network  
![
](https://lh3.googleusercontent.com/63Z01sBAxg6JNrj5Sq6z7GKSMDuEl1fIeIwrugfqCQ_9rZI9CBeVgvABg1Ay0L482MCC2TihNt1C "wae7")  

Prior Network  
![
](https://lh3.googleusercontent.com/IP3NaboGIu3DTnb3PYBoQoJKyY6lS3zB5ec11iKtsxau8_ch6gvZ2PzHBNJYV3mh57TLjYdvpURH "wae8")  

decoder  
![
](https://lh3.googleusercontent.com/QOuW4ehP7kkre8QilG_qLFNcCVjOUerOpmbpxB7m3O0H9iQmq_BlqGHXc3KGFM8moavTYPyHpwLa "wae9")  


**References**  
[Paper](https://arxiv.org/abs/1805.12352)  
[Code](https://github.com/guxd/DialogWAE)  

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE4NTA0NjUzNiwtMjMwNzk3NTM1XX0=
-->