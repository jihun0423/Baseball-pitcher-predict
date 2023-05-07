# Baseball-pitcher-predict

데이터 출처 : https://baseballsavant.mlb.com/leaderboard/custom?year=2022&type=batter&filter=&sort=1&sortDir=desc&min=q&selections=xba,xslg,xwoba,xobp,xiso,exit_velocity_avg,launch_angle_avg,sweet_spot_percent,barrel_batted_rate,&chart=false&x=xba&y=xba&r=no&chartType=beeswarm  


<br />


# 1. 개요
다른 분석 프로젝트나 대회를 하다가 잠시 마음을 돌리고 쉬고싶어 평소 좋아하던 야구에 관해 짧은 예측을 해보기로 하였다.  
메이저리그 투수의 수비 및 운과 무관한 2023시즌의 성적을 예측해 보았다.  



<br />



# 2. 참여 인원 / 기간
* 개인 프로젝트
* 2023년 5월 1일 ~ 2023년 5월 4일


<br />


# 3. 사용 기술
* Python
* SQL
* Matplotlib
* Sklearn
* Pycaret


<br />


# 4. 분석 하고자 하는 대상
* 2023시즌에 메이저리그에서 활동중인 투수들의 성적을 이전 성적들을 바탕으로 예측해보고 싶었다. 이를 위해, 2023년 전에 활약을 했던 선수들 중 현재까지도 현역인 선수들만을 골라 대상으로 하였다
* 분석하고자 하는 성적의 지표는 xwOBA로, 보통 투수의 성적이라 한다면 야구라는 스포츠의 특성상 타구가 맞았을 때 수비수들이 수비를 얼마나 잘하는지, 그 날의 바람 상태나 환경때문에 운이 나쁘게 안타나 홈런이 되었다던지 하는 운과 수비의 요소가 반드시 반영이 된다. xwOBA는 이러한 수비와 운을 완전히 배제한 성적으로, 팀이나 환경에 상관없이 순전히 투수의 능력만을 중립적으로 알 수 있게 해주는 지표이다.
* 이러한 지표가 가능한 이유는 야구에 BABIP이라는 이론이 존재하기 때문인데, 어떤 투수가 던진 공이던 그 공이 타자의 배트에 맞았을 때 일어나는 상황들의 확률은 동등하다는 이론이다.  
메이저리그에서도 매우 뛰어난 성적을 거두는 투수와, 방출 위기에까지 놓인 성적이 좋지 않은 투수의 '공이 배트에 맞았을 때 일어나는 상황들의 확률'이 동일하다는 이 이론은, 처음에는 반발이 심하였지만 통계상 거의 사실인 것으로 드러났다. 따라서, 이 이론을 바탕으로 여러가지 통계 지표가 생겨났고, 이번에 사용하고자 하는 xwOBA도 그렇다.



<br />



# 5. 분석 방법
* 야구는 다른 스포츠보다도 1년마다의 성적이 매우 다른 스포츠라고 생각한다. 작년까지만 해도 엄청난 에이스였던 선수가 아무 징조 없이 갑자기 무너지는 모습은 야구에선 드물지 않은 일이다. 그러나 통계에서 예측을 할 경우에는, 저런 예외적인 상황들을 제외하고 통상적인 상황들을 예측해야 한다고 생각한다. 
* 따라서, 2023시즌 이전의 최근 3년간의 성적을 통해 예측을 할 예정이고, 가장 최근의 성적에 더 많은 가중치를 두어 학습하고자 한다.
* 2016~2022시즌 까지의 선수들의 기록들을 바탕으로 성적을 예측하는 모델을 학습 시킨 뒤 (train),  
2023 시즌의 실제 기록을 통하여 구한 예측 성적과 실제 성적을 비교하여 모델이 적합한지를 평가하고 (Valid),  
2023 시즌의 선수들의 기록을 이전 시즌의 성적들로 예측하여 이 예측한 기록들을 모델에 대입하여 예상 성적을 구한다. (Test)
* 이렇게 해서 예측한 성적보다 매우 좋게 나왔거나, 매우 안좋게 나온 경우에 대해서 원인을 파악해볼 예정이다.



<br />


# 6. 진행  
