# 0. 用前须知

### 任何国家，地区，组织和个人使用此项目必须遵守以下法律

#### 《[民法典](http://gongbao.court.gov.cn/Details/51eb6750b8361f79be8f90d09bc202.html)》

#### 第一千零一十九条

任何组织或者个人**不得**以丑化、污损，或者利用信息技术手段伪造等方式侵害他人的肖像权。**未经**肖像权人同意，**不得**制作、使用、公开肖像权人的肖像，但是法律另有规定的除外。**未经**肖像权人同意，肖像作品权利人不得以发表、复制、发行、出租、展览等方式使用或者公开肖像权人的肖像。对自然人声音的保护，参照适用肖像权保护的有关规定。
**对自然人声音的保护，参照适用肖像权保护的有关规定**

#### 第一千零二十四条

【名誉权】民事主体享有名誉权。任何组织或者个人**不得**以侮辱、诽谤等方式侵害他人的名誉权。

#### 第一千零二十七条

【作品侵害名誉权】行为人发表的文学、艺术作品以真人真事或者特定人为描述对象，含有侮辱、诽谤内容，侵害他人名誉权的，受害人有权依法请求该行为人承担民事责任。行为人发表的文学、艺术作品不以特定人为描述对象，仅其中的情节与该特定人的情况相似的，不承担民事责任。

#### 《[中华人民共和国宪法](http://www.gov.cn/guoqing/2018-03/22/content_5276318.htm)》|《[中华人民共和国刑法](http://gongbao.court.gov.cn/Details/f8e30d0689b23f57bfc782d21035c3.html?sw=中华人民共和国刑法)》|《[中华人民共和国民法典](http://gongbao.court.gov.cn/Details/51eb6750b8361f79be8f90d09bc202.html)》|《[中华人民共和国合同法](http://www.npc.gov.cn/zgrdw/npc/lfzt/rlyw/2016-07/01/content_1992739.htm)》

## 0.1 使用规约

> [!WARNING]
>
> 1. **本教程仅供交流与学习使用，请勿用于违法违规或违反公序良德等不良用途。出于对音源提供者的尊重请勿用于鬼畜用途**
> 2. **继续使用视为已同意本教程所述相关条例，本教程已进行劝导义务，不对后续可能存在问题负责**
> 3. **请自行解决数据集授权问题，禁止使用非授权数据集进行训练！任何由于使用非授权数据集进行训练造成的问题，需自行承担全部责任和后果！与仓库、仓库维护者、svc develop team、教程发布者无关！**

具体使用规约如下：

- 本教程内容仅代表个人，均不代表 so-vits-svc 团队及原作者观点
- 本教程默认使用由 so-vits-svc 团队维护的仓库，涉及到的开源代码请自行遵守其开源协议
- 任何发布到视频平台的基于 sovits 制作的视频，都必须要在简介明确指明用于变声器转换的输入源歌声、音频，例如：使用他人发布的视频或音频，通过分离的人声作为输入源进行转换的，必须要给出明确的原视频、音乐链接；若使用是自己的人声，或是使用其他歌声合成引擎合成的声音作为输入源进行转换的，也必须在简介加以说明。
- 请确保你制作数据集的数据来源合法合规，且数据提供者明确你在制作什么以及可能造成的后果。由输入源造成的侵权问题需自行承担全部责任和一切后果。使用其他商用歌声合成软件作为输入源时，请确保遵守该软件的使用条例。注意，许多歌声合成引擎使用条例中明确指明不可用于输入源进行转换！
- 云端训练和推理部分可能涉及资金使用，如果你是未成年人，请在获得监护人的许可与理解后进行，未经许可引起的后续问题，本教程概不负责
- 本地训练（尤其是在硬件较差的情况下）可能需要设备长时间高负荷运行，请做好设备养护和散热措施
- 出于设备原因，本教程仅在 Windows 系统下进行过测试，Mac 和 Linux 请确保自己有一定解决问题能力
- 继续使用视为已同意本仓库 README 所述相关条例，本仓库 README 已进行劝导义务，不对后续可能存在问题负责。

# 1. 分离伴奏人声

## 1.1 使用在线MVSep_MDX23分离人声伴奏

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/yh-hacker/svc-online/blob/main/mvsep_mdx23.ipynb)

## 1.2 离线UVR5去和声混响
#### 去混响【3选1，根据混响的程度选择，没有混响直接跳过】：
    VR Architecture：UVR-De-Echo-Normal选No Echo Only（轻度混响）
    VR Architecture：UVR-De-Echo-Aggressive选No Echo Only（重度混响）
    VR Architecture：UVR-De-Echo-Dereverb选No Reverb Only（遇到鸟之诗这种变态的混响可以用）

#### 去和声【3选1，没有和声直接跳过】：
    VR Architecture：UVR-BVE-4B_SN-44100-1选Instrumental Only
    VR Architecture：5_HP_Karaoke-UVR选Vocals Only （比6激进，有可能会扣过头）
    VR Architecture：6_HP_Karaoke-UVR选Vocals Only（没有5激进）

## 1.3 完成以上三去除后得到干净的人声，方可进行下一步操作

# 2. 转换人声(任选其一）

## 2.1 在线转换 ———— On Colab （极快，不过可能受限）
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/yh-hacker/svc-online/blob/main/mvsep_mdx23.ipynb)

## 2.2 在线转换 ———— On Huggingface （较慢）
[![Hugging Face Spaces](https://img.shields.io/badge/SVC-ykt?style=for-the-badge)](https://huggingface.co/spaces/YH-Official/SVC-ykt)

## 2.3 本地转换 ———— 技术难度过大，再次不过多赘述
