

## CogACT �� Action Head ������

CogACT ��һ���ں�����ģ����Ӿ�-����-������VLA��ģ�ͣ��� **Action Head** ����**������ɢģ�ͣ�Conditional Diffusion Model��** ʵ�֣��������ģ�����ɵĸ߲������ token �Ͷ�ģ̬�۲죬���ɸ߾��ȵ���������������֧�ָ��Ӳ�������͸�ʱ���������

---

### һ������˼��

CogACT ��������ģ���̷�Ϊ���׶Σ�

| �׶�             | ˵��                                                           |
|------------------|----------------------------------------------------------------|
| �Իع�׶�        | ʹ�� LLM ����ģ���������� token ��Ϊ����������                     |
| �������ɽ׶Σ�Action Head�� | ʹ��**Latent Diffusion Policy Head**���������ı������Ϊ������������ |

�ö���ͷ���ñ�׼�� **DDPM��Denoising Diffusion Probabilistic Model��** ��ܣ���ͨ������ģ����м��ʾ�����������ƣ�֧�ֶ��ֻ����˿������͡�

---

### ��������ͷ�ṹ�����

#### ������ģ��ʽ

- ʹ��һ��**Latent Diffusion Decoder**���� Transformer �����������ʾ����Ϊ������
- ����ά�Ȱ���������ĩ��ִ������λ��/��̬/��צ״̬�ȣ�
- ÿ������һ�������� joint-space ���������������ڶ�� robot embodiment����

#### ����ṹ��

- **Transformer Encoder**�������Ӿ������ԡ���ģ̬���룩��
- **Diffusion Policy Decoder**���������ɲ��֣���
  - ��׼ DDPM �ṹ��
  - ��������Ϊ LLM reasoning tokens��
  - �����������ά�ȿɱ䣨���ݻ����ֱ����ɶȣ���
  - ���һ��Ϊ **MLP �� Joint Space ��������**��

#### ����ģ��ע�룺

- �� reasoning ģ����������� token ע�뵽 Transformer ��������
- ʹ�� FiLM��Feature-wise Linear Modulation����ʽʵ��ģ����أ�
- ���⽫ reasoning �����Ϊֱ�� token����������Ч�����ȶ��ԡ�

---

### ����ѵ������������

#### ѵ���׶Σ�

- �������������γ� latent��
- ʹ�� diffusion decoder Ԥ�������� denoising vector��
- �Ż� DDPM ��ʧ��
  \[
  \mathcal{L}_{\text{diff}} = \mathbb{E}[\|\epsilon - \epsilon_\theta(x_t, c)\|^2]
  \]

#### ����׶Σ�

- ������ǰ�Ӿ��۲� + �����ı���
- LLM reasoning �� Transformer token embedding��
- DDPM �ಽ�������� latent �� Ԥ�� robot joint ���ƶ�����

---

### �ġ�������ģ�ͶԱȣ�Action Head��


| ģ��         | Action Head ����                     | �Ƿ��Իع� | �Ƿ��������� | �������� | ģ��ṹ                     |
|--------------|----------------------------------------|--------------|----------------|------------|------------------------------|
| RT-2         | token-based autoregressive             | ��           | ��             | ��         | ͳһ�ṹ                     |
| OpenVLA      | token �� De-Tokenizer                   | ��           | ��            | ��         | ��������ռ�                 |
| Octo         | MLP + Diffusion Chunk Decoder          | ��          | ����          | ��         | ����ṹ������ readout��     |
| ��0           | Flow Matching + Action Expert          | ��          | ��             | ��         | **VLM + ר�ö���ģ�����**    |
| **CogACT**   | **LLM reasoning + Diffusion Head**     | ��          | �ǣ�������ǿ�� | **��**     | **LLM + Diffusion ����ṹ** |


---


### �塢��������ܽ�

- **����-��������ܹ�**������ token ���ٲ��붯�����������³������Ч�ʣ�
- **�߾�����ɢ����**����Ȼع�/token������ƽ�������ܽ�ģ���������ԣ�
- **�ɽ��� reasoning ����**��LLM reasoning ������ӻ���֧�ִ����������ԣ�
- **�� embodiment ����**��ͨ���л� MLP ��������䲻ͬ�����˽ṹ��
- **���΢������**���ɵ���΢�� reasoning ģ���������ģ�顣

