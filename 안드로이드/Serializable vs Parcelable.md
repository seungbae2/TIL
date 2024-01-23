# Serializable vs Parcelable

Serializable 

객체를 byte 형태로 변환시키는 기술 

액티비티간 또는 서비스간 데이터를 주고 받는 용도

byte를 다시 객체로 변환할 때 JVM 내부에서 임시 객체를 많이 만듬 → 성능에 영향을 미침

Parcelable

안드로이드 SDK에 포함하는 인터페이스

Serializable의 성능저하를 보완하기 위해 만들어짐 → 변환하는 부분을 개발자가 직접 구현