---
title:  "[AWS Solution Architect] Block Storage vs Object Storage vs File Storage"
date: 2022-1-26 2:36PM
excerpt: "aws"

author: Yuha
categories: [Development, AWS]
tags: [aws, certification, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-1-26 2:36PM
---


### 서로 다른 방식으로 데이터를 저장하고 검색

---

### Block storage
- SAN(Storage Area Network) 또는 클라우드 기반 스토리지 환경에 데이터 파일을 저장하는 데 사용되는 기술
- 빠르고 효율적이며 안정적인 데이터 전송이 요구되는 컴퓨팅 상황의 경우 블록 스토리지를 선호
- 데이터를 블록으로 분할한 후, 해당 블록을 각각 고유 ID를 지닌 개별 조각으로 저장
- 사용자 환경으로부터 데이터를 디커플링함으로써 해당 데이터가 다수의 환경에서 분산될 수 있도록 허용합니다. 이렇게 되면 데이터에 대한 다수의 경로가 만들어지며, 사용자는 이를 통해 데이터를 빠르게 검색할 수 있습니다.
- VMFS를 저장하기 위한 블록 기반 스토리지 볼륨을 손쉽게 만들어서 이를 포맷할 수 있습니다. 그리고 물리적 서버가 해당 블록에 연결됨으로써 다수의 가상 머신을 구축할 수 있습니다. 게다가, 블록 기반 볼륨을 구축하고 운영체제를 설치한 후 해당 볼륨에 연결함으로써 사용자는 이러한 기본 운영체제를 사용하여 파일을 공유할 수 있습니다.

---

### Object Storage
- 데이터 파일을 오브젝트라고 하는 조각들로 분할, 단일 저장소에 해당 오브젝트를 저장. 다수의 네트워킹 시스템 간에 분산될 수 있습니다.
- 실제로 애플리케이션에서 모든 오브젝트를 관리하므로, 기존의 파일 시스템은 더 이상 필요가 없습니다. 각 오브젝트는 애플리케이션이 오브젝트 식별에 사용하는 고유 ID를 수신합니다. 그리고 각 오브젝트는 오브젝트에 저장된 파일에 대한 정보인 메타데이터를 저장합니다.


*** Difference of block storage and object storage
- 각 스토리지가 메타데이터를 처리하는 방법
- block storage
    : 메타데이터가 기본 파일 속성으로 제한됨
    : 파일을 변경하면 새로운 오브젝트가 생성되어서 자주 변경되지 않는 정적 파일에 가장 적합

- object storage
    : 오브젝트에 저장된 <b>데이터 파일에 관한 추가적인 상세 정보</b>를 포함하도록 <b>메타데이터를 사용자 정의</b>할 수 있습니다

---

### File Storage
- NAS(Network Attached Storage) 기술과 밀접한 관련
- 기존의 네트워크 파일 시스템과 동일한 개념을 사용하여 사용자와 애플리케이션에 스토리지를 제공
- 사용자나 애플리케이션은 디렉토리 트리, 폴더 및 개별 파일을 통해 데이터를 수신
    - <b>구성하기는 매우 쉽지만</b>, <b>데이터에 대한 액세스가 데이터에 대한 단일 경로로 제한됨</b>으로 인해 블록 스토리지나 오브젝트 스토리지에 비해 <b>성능이 떨어질 수 있습니다</b>
- Windows용 NTFS(New Technology File System) 또는 Linux용 NFS(Network File System) 등의 <b>공통 파일 레벨 프로토콜</b>에서만 작동됩니다. 이로 인해 서로 다른 시스템 간에 가용성이 제한될 수 있음

<br>

<https://www.ibm.com/kr-ko/cloud/learn/block-storage>