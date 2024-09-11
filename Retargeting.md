- 리타겟 과정 기록 </br>
애니메이션은 적용 Skeleton이 다르면 사용할 수 없으므로 각 Skeleton에 맞게 리타겟을 해주어야 한다.

# 1. Blender를 사용해 .pmx 파일을 fbx로 변환한다.
## 1-1. Blender에서 pmx 파일을 사용할 수 있게 mmd_tools라는 플러그인을 다운로드해 임포트한다.
최신버전 : 
https://mmd-blender.fandom.com/wiki/MMD_Tools
사이트에 plugIn을 추가하는 방법이 영상으로 설명되어 있다.

다른 버전(최신 버전은 Blender의 4.2LTS를 지원한다. 다른 버전은 이 링크로) :
https://github.com/UuuNyaa/blender_mmd_tools?tab=readme-ov-file
프로젝트를 다운 받은 후 압축을 해제한다.
2.82 기준 Edit -> Preferences -> Add-ons에서 Install을 선택. 
압축해제 경로로 가서 내부의 mmd_tools 폴더를 선택한 후 Install Add-on을 선택한다.
성공적으로 인스톨되었다면 Edit -> Preferences -> Add-ons의 검색창에 mmd를 검색하는 것으로 mmd_tools가 나타날 것이다.
체크박스를 눌러서 활성화 해준다.

당시에 여러버전으로 시도해보다 결국 Blender 4.2 버전을 사용했다.

## 1-2. .pmx 임포트 후 본 이름 번역
![bandicam 2024-09-11 22-54-49-610](https://github.com/user-attachments/assets/ef3fcf1c-e700-4251-9fa9-19d8d4bab5c6)

PlugIn이 정상적으로 활성화 되었다면 이미지와 같이 MikuMikuDanceModel이 임포트 선택지에 추가된다. 이것을 선택해 목표로하는 모델을 가져온다.

![bandicam 2024-09-11 22-58-44-988](https://github.com/user-attachments/assets/d0f8c50a-a049-4fb8-9731-9ea2aec8743a)

종종 본 이름이 영어가 아닌 일본어나 중국어로 되어 있는 경우가 있을 것이다. MMD에 자동번역을 지원하는 기능이 있는 것 같지만 내가 사용한 모델은 Mihoyo의 게임인 붕괴 StarRail의 Gallagher였다
중국어는 번역기능이 없어 직접 일일히 찾아가며 번역을 해주었다.

![bandicam 2024-09-11 23-00-02-885](https://github.com/user-attachments/assets/520cacb6-674e-4ea3-a615-c54557f66cf9)

본 이름 수정은 본을 더블 클릭 후 직접 수정했다. 후에 Name(English)를 지정한 뒤 일괄 번역을 할 수도 있겠다는 생각이 들었지만 시도해 보진 않았다.
후에 다른 모델을 수정할 일이 있을 때 해보는 것으로..

![bandicam 2024-09-11 23-04-44-003](https://github.com/user-attachments/assets/bb0a07e4-abc6-4b71-a65e-7d87a5299584)

개인적은 Blender의 Edit Mode에서 본 이름을 수정하는 것을 추천한다. Object Mode에서 본을 선택하면 전체 본에 하이라이트가 들어와 현재 선택한 본이 어떤 본인지 알 수 없지만, EditMode로 하면 선택한 본만 하이라이트가 들어온다.

## 1-3. 본 이름을 수정한 후에는 .fbx로 Export를 해준다.
![bandicam 2024-09-11 23-06-30-324](https://github.com/user-attachments/assets/e68d01ce-84fa-4024-a775-b06f03e33c7b)

Export시 주의할 점은 이미지에 나와있는 것처럼 Amature과 Mesh만 선택된 채로 Export하는 것이다. 다른 것이 같이 Export되면 모델이 망가지는 것을 확인했다.

# 2. Unreal에 임포트 후 머테리얼 정돈
이제 .fbx 파일을 만들었으니 Unreal에 임포트할 차례다.
Unreal Project를 열고 fbx를 임포트할 폴더를 연 뒤 임포트 버튼을 눌러준다. 
다른 .fbx 모델을 임포트하는 것과 같이 임포트를 해주면 된다. 

![bandicam 2024-09-11 23-16-23-134](https://github.com/user-attachments/assets/2f2b2233-cc9d-4499-961b-3099815e37a6)

일단 Import Mesh와 SkeletalMesh는 체크가 되어 있어야 하고, 모델에 따라서는 Use T0As Ref Pose를 켜주어야 할 수도 있다.

임포트가 되었으니 이제 리타겟을 할 차례인가 싶겠지만.. 아닐 것이다.

![bandicam 2024-09-11 23-19-53-456](https://github.com/user-attachments/assets/728de990-c09a-46f5-8e30-229f83dcf70c)

높은 확률로 머테리얼이 깨져있다. .pmx에서 .fbx로 변환되는 도중에 머티리얼 정보가 소실되는 것으로 추정된다. 각 부위에 머티리얼 이름은 남아있는 것 같은데 정작 머티리얼을 열어보면 확인해보면 그냥 하얀색이다.
이럴 경우 .pmx에 사용된 텍스쳐를 가져다 새로 머테리얼을 만들고 적용시켜야 한다. .pmx에 사용된 텍스쳐는 보통 해당 모델이 존재하는 폴더나 그 상위 폴더에 같이 존재하니 찾아보길 바란다.

![bandicam 2024-09-11 23-22-58-952](https://github.com/user-attachments/assets/0b722540-9a01-4437-846e-2710428f8421)
![bandicam 2024-09-11 23-22-37-230](https://github.com/user-attachments/assets/4f9c7b6d-3372-4e9a-8d22-70859b4086d5)
![bandicam 2024-09-11 23-22-13-447](https://github.com/user-attachments/assets/999244fb-28bc-4be0-ab81-15a8354aaee8)

여튼 텍스쳐를 가져와 임포트하고 머테리얼을 만들고 적용시켰다. 이제 리타겟을 시작할 차례다.

# 3. 본 정보 수정
## 3-1. 본 리타겟 준비
임포트한 모델의 Skeleton 파일을 열고 라타깃 메니저 창을 연다.

![bandicam 2024-09-11 23-26-30-657](https://github.com/user-attachments/assets/fe37fbbc-b0df-4e71-a4c6-09662bee4da9)

![bandicam 2024-09-11 23-32-30-721](https://github.com/user-attachments/assets/85a45eda-706a-4f58-9f88-50123c3d3158)

리타겟 메니저 창을 열면 이미지와 같이 릭 셋업이란 것이 존재한다. 이 릭은 본 구조에 대한 번역기? 매칭 데이터 같은 것이라 생각하면 된다.
이 릭 중 Humanoid는 Unreal에서 제공하는 기본 인간형 릭으로 Unreal이 다른 인간형 모델들도 이 릭을 사용하니 인간형 모델을 사용한다면 이 릭을 선택한다.

## 3.2. 본 매칭

![bandicam 2024-09-11 23-28-30-743](https://github.com/user-attachments/assets/84f3deae-46ef-4801-b365-048ac43256a0)

릭을 선택하면 다음과 같이 어떤 본을 지정해줘야 하는지 표시를 해준다. 각 부위에 맞는 본을 찾아서 선택을 해준다. Unreal5에서는 더 편리한 리타겟 기능을 지원해준다고 하지만 현재 사용중인 버전은 4.25이니 노가다를 해줘야 한다.

## 3-3. 기본 포즈 일치시키기
본을 매칭시켰다고 다 끝난 것이 아니다. 이제는 각 본의 위치를 일치시켜줘야 한다. 완전히 똑같을 필요는 없지만 비슷하게라도 맞춰야 한다.
그렇지 않다면..

![bandicam 2024-09-11 23-36-58-064](https://github.com/user-attachments/assets/adcdb47b-06b5-4df6-98e4-89d15a144ee5)
![bandicam 2024-09-11 23-37-08-297](https://github.com/user-attachments/assets/8f409f34-2933-4731-9610-37773011f373)
![bandicam 2024-09-11 23-37-14-948](https://github.com/user-attachments/assets/4dfe4397-d4ff-477f-8897-6989e21b0efd)

모델이 어이없게 망가지는 모습을 볼 수 있다.

포즈를 일치시킬 때는 리타겟할 모델을 참조 모델에 포즈에 일치시켜줘야 한다.
여기서 리타겟할 모델은 Gallagher이고 참조 모델은 Unreal 기본 Mannequine이니 Mannequine의 기본 포즈에 Gallagher을 일치시켜야 한다.

![bandicam 2024-09-11 23-39-34-825](https://github.com/user-attachments/assets/029a542b-0dee-451a-9acd-a133ce6257f4)

리카겟 매니저 하단에서 포즈 숨김으로 만들고 포즈를 일치시켜준 뒤 해당 포즈 사용을 눌러줘야 한다. 포즈를 숨기으로 하지 않으면 아예 모델의 기본 포즈가 바뀌어 버리고 현재 포즈 사용을 눌러주지 않으면 변경된 내용이 적용되지 않는다.
임시 포즈를 만들어 사용하는 느낌인 것 같다.

본 위치 수정 전

![bandicam 2024-09-11 23-44-40-809](https://github.com/user-attachments/assets/2b5912f2-136a-464a-8605-74e0709aa4df)

본 위치 수정 후

![bandicam 2024-09-11 23-44-48-084](https://github.com/user-attachments/assets/682392e9-bf16-4e9a-af8b-5c554b7be5f6)

아 참!

![bandicam 2024-09-11 23-42-00-788](https://github.com/user-attachments/assets/31bf3be7-14f2-47a8-9d2e-116d5480f486)

스켈레톤 메시 창에서 프리뷰 셋팅을 보면 메시 부분의 Preview Mesh 아래에 버튼이 하나 있을 것이다. 이미지에서는 이미 눌러서 없지만 해당 버튼을 눌러주지 않으면 리타겟을 할 수가 없게 되니 주의해야 한다.

# 4. 애니메이션 리타겟팅
이제 본에 맞게 애니메이션을 리타겟 해주어야 한다. 
애니메이션 리타겟은 Animation파일 Anim Montage파일, Animation Blueprint에 할 수 있다.

![bandicam 2024-09-12 00-01-41-826](https://github.com/user-attachments/assets/8e12b6f7-c8f6-4a70-837e-f02546e8d387)
![bandicam 2024-09-12 00-02-00-487](https://github.com/user-attachments/assets/f9693ac8-89b0-40d2-9f36-32fff9bed63a)
![bandicam 2024-09-12 00-02-28-523](https://github.com/user-attachments/assets/ba220e23-1c1d-4bb3-a1b7-fbe4196d3532)

참조 파일(새 모델에 적용하고 싶은 애닝메이션)에 우클릭 후 oo 리타깃-> oo 복제 후 리타깃을 선택하면 원본 파일을 남기고 복제된 리타겟 파일을 생성할 수 있다.

![bandicam 2024-09-12 00-06-54-110](https://github.com/user-attachments/assets/5f59f047-e7f5-45a3-9319-dd51fc90eaf5)

복제 후 리타깃을 선택하면 나오는 창에서 리타겟 대상인 Skeletond르 고르고 저장 경로를 지정한 뒤 리타깃을 누르면 된다.
복제된 파일은 내부 설정은 그대로 이고 타깃만 선택한 Skeleton으로 변경된다. 때문에 Animation Blueprint의 경우 BlendBone이나 Slot의 본 이름 같은 설정들은 직접 변경해 주어야한다.
리타겟 시 Montage에 경우에는 Animation이 같이 복제 후 리타겟 되고 애니메이션 블루 프린트 같은 경우에는 해당 Animation BluePrint에서 사용중인 Animation과 BlendSpace, 그 BlendSpace에서 사용 중인 Animation이 같이 리타겟 후 복제된다! 


Animation Blueprint 리타겟 후 저장된 모습

![bandicam 2024-09-12 00-12-37-973](https://github.com/user-attachments/assets/85bc8763-3464-4f0f-99ac-859fc529debc)


### 참고자료
#### 영상
https://www.youtube.com/watch?v=5mSsvwvT9m0&list=PLFb8xU8hLIoCO3ZS3jImWb48BYzIgZ0Ab&index=1
https://www.youtube.com/watch?v=4846reyRgLY&list=PLFb8xU8hLIoCO3ZS3jImWb48BYzIgZ0Ab&index=2
https://www.youtube.com/watch?v=nWoHufw6k9s&list=PLFb8xU8hLIoCO3ZS3jImWb48BYzIgZ0Ab&index=3
#### BelnderPluginDownload
https://mmd-blender.fandom.com/wiki/MMD_Tools
