clear all   %清除workspace
clc  
tic  
addpath('C:\Users\gg90180\Desktop\論文\TEJ Data')

%% 併入下期價格
load DataVARI.mat
xlswrite('DataVARI.xlsx',DataVARI);
Data=cell2mat(DataVARI(2:end,:));
data=sortrows(Data,1);
%3.SIZE 4.LEVERAGE 5.BM Ratio 6.IVOL 7.momemtum 8.Illiq 9.MAX
%10.ASVI 11.RET 12.Price

RETall=[];
corID=unique(data(:,1));
for id=1:size(corID,1)
    iiD=data(find(data(:,1)==corID(id,1)),:);
    x=iiD(1:end-1,:);
    
    iiDretAll=[];
    [a,b]=size(x);
    for i=1:a
        iiDret=horzcat(x(i,:),iiD(i+1,b));
        iiDretAll=vertcat(iiDretAll,iiDret);
    end
    RETall=vertcat(RETall,iiDretAll);
end
%3.SIZE 4.LEVERAGE 5.BM Ratio 6.IVOL 7.momemtum 8.Illiq 9.MAX
%10.ASVI 11.RET 12.Price 13.Price(t+1)

%計算下期報酬
a=(RETall(:,13)-RETall(:,12))./RETall(:,12);
RETall=horzcat(RETall,a);
%3.SIZE 4.LEVERAGE 5.BM Ratio 6.IVOL 7.momemtum 8.Illiq 9.MAX
%10.ASVI 11.RET 12.Price 13.Price(t+1) 14.RET(t+1)

%% 併入下期momemtum
load DataVARI.mat
Data=cell2mat(DataVARI(2:end,:));
data=sortrows(Data,1);
%3.SIZE 4.LEVERAGE 5.BM Ratio 6.IVOL 7.momemtum 8.Illiq 9.MAX
%10.ASVI 11.RET 12.Price

MOMall=[];
corID=unique(data(:,1));
for id=1:size(corID,1)
    iiD=data(find(data(:,1)==corID(id,1)),:);
    x=iiD(1:end-1,:);
    
    iiDmomAll=[];
    [a,b]=size(x);
    for i=1:a
        iiDmom=horzcat(x(i,:),iiD(i+1,7));
        iiDmomAll=vertcat(iiDmomAll,iiDmom);
    end
    MOMall=vertcat(MOMall,iiDmomAll);
end
%3.SIZE 4.LEVERAGE 5.BM Ratio 6.IVOL 7.momemtum 8.Illiq 9.MAX
%10.ASVI 11.RET 12.Price 13.momemtum(t+1)

%將下期mom併入
RETall=horzcat(RETall(:,2)*10000+RETall(:,1),RETall); 
MOMall=horzcat(MOMall(:,2)*10000+MOMall(:,1),MOMall); 
for i=1:size(MOMall,1)
    b=find(MOMall(i,1)==RETall(:,1));
    RETall(b,16)=MOMall(i,14);
end
RETall(:,1)=[];
%3.SIZE 4.LEVERAGE 5.BM Ratio 6.IVOL 7.momemtum 8.Illiq 9.MAX
%10.ASVI 11.RET 12.Price 13.Price(t+1) 14.RET(t+1) 15.MOM(t+1)

%去除2010資料
RETall=horzcat(floor(RETall(:,2)./100),RETall);
RETall=RETall(find(RETall(:,1)~=2010),:); %去除2010資料
RETall(:,1)=[];
save RETall RETall

%% MAX分組1(低)
load RETall
RETall(:,9)=RETall(:,9)./100;
rank1=[];
Date=unique(RETall(:,2));
for D=1:size(Date,1)
    x1=RETall(find(RETall(:,2)==Date(D,1)),:); %抓出其中一個月份
    
    RankONE=[];
    q1=prctile(x1(:,9),[10,20,30,40,50,60,70,80,90]);
    uni1=unique(x1(find(x1(:,9)<q1(1,1)),1)); %當月份小於第10百分位數的位置
    for i=1:size(uni1,1)
        abc=x1(find(x1(:,1)==uni1(i,1)),:);
        ab=horzcat(abc,1);
        RankONE=vertcat(RankONE,ab);
    end
    rank1=vertcat(rank1,RankONE);
end

save rank1 rank1
clear all   %清除workspace
clc  
tic  

%% MAX分組2
load RETall
RETall(:,9)=RETall(:,9)./100;
rank2=[];
Date=unique(RETall(:,2));
for D=1:size(Date,1)
    x1=RETall(find(RETall(:,2)==Date(D,1)),:); %抓出其中一個月份
    
    RankONE=[];
    q1=prctile(x1(:,9),[10,20,30,40,50,60,70,80,90]);
    uni1=unique(x1(find(x1(:,9)>=q1(1,1)&x1(:,9)<q1(1,2)),1)); 
    for i=1:size(uni1,1)
        abc=x1(find(x1(:,1)==uni1(i,1)),:);
        ab=horzcat(abc,2);
        RankONE=vertcat(RankONE,ab);
    end
    rank2=vertcat(rank2,RankONE);
end

save rank2 rank2
clear all   %清除workspace
clc  
tic  

%% MAX分組3
load RETall
RETall(:,9)=RETall(:,9)./100;
rank3=[];
Date=unique(RETall(:,2));
for D=1:size(Date,1)
    x1=RETall(find(RETall(:,2)==Date(D,1)),:); %抓出其中一個月份
    
    RankONE=[];
    q1=prctile(x1(:,9),[10,20,30,40,50,60,70,80,90]);
    uni1=unique(x1(find(x1(:,9)>=q1(1,2)&x1(:,9)<q1(1,3)),1)); 
    for i=1:size(uni1,1)
        abc=x1(find(x1(:,1)==uni1(i,1)),:);
        ab=horzcat(abc,3);
        RankONE=vertcat(RankONE,ab);
    end
    rank3=vertcat(rank3,RankONE);
end

save rank3 rank3
clear all   %清除workspace
clc  
tic  

%% MAX分組4
load RETall
RETall(:,9)=RETall(:,9)./100;
rank4=[];
Date=unique(RETall(:,2));
for D=1:size(Date,1)
    x1=RETall(find(RETall(:,2)==Date(D,1)),:); %抓出其中一個月份
    
    RankONE=[];
    q1=prctile(x1(:,9),[10,20,30,40,50,60,70,80,90]);
    uni1=unique(x1(find(x1(:,9)>=q1(1,3)&x1(:,9)<q1(1,4)),1)); 
    for i=1:size(uni1,1)
        abc=x1(find(x1(:,1)==uni1(i,1)),:);
        ab=horzcat(abc,4);
        RankONE=vertcat(RankONE,ab);
    end
    rank4=vertcat(rank4,RankONE);
end

save rank4 rank4
clear all   %清除workspace
clc  
tic  

%% MAX分組5
load RETall
RETall(:,9)=RETall(:,9)./100;
rank5=[];
Date=unique(RETall(:,2));
for D=1:size(Date,1)
    x1=RETall(find(RETall(:,2)==Date(D,1)),:); %抓出其中一個月份
    
    RankONE=[];
    q1=prctile(x1(:,9),[10,20,30,40,50,60,70,80,90]);
    uni1=unique(x1(find(x1(:,9)>=q1(1,4)&x1(:,9)<q1(1,5)),1)); 
    for i=1:size(uni1,1)
        abc=x1(find(x1(:,1)==uni1(i,1)),:);
        ab=horzcat(abc,5);
        RankONE=vertcat(RankONE,ab);
    end
    rank5=vertcat(rank5,RankONE);
end

save rank5 rank5
clear all   %清除workspace
clc  
tic  

%% MAX分組6
load RETall
RETall(:,9)=RETall(:,9)./100;
rank6=[];
Date=unique(RETall(:,2));
for D=1:size(Date,1)
    x1=RETall(find(RETall(:,2)==Date(D,1)),:); %抓出其中一個月份
    
    RankONE=[];
    q1=prctile(x1(:,9),[10,20,30,40,50,60,70,80,90]);
    uni1=unique(x1(find(x1(:,9)>=q1(1,5)&x1(:,9)<q1(1,6)),1)); 
    for i=1:size(uni1,1)
        abc=x1(find(x1(:,1)==uni1(i,1)),:);
        ab=horzcat(abc,6);
        RankONE=vertcat(RankONE,ab);
    end
    rank6=vertcat(rank6,RankONE);
end

save rank6 rank6
clear all   %清除workspace
clc  
tic  

%% MAX分組7
load RETall
RETall(:,9)=RETall(:,9)./100;
rank7=[];
Date=unique(RETall(:,2));
for D=1:size(Date,1)
    x1=RETall(find(RETall(:,2)==Date(D,1)),:); %抓出其中一個月份
    
    RankONE=[];
    q1=prctile(x1(:,9),[10,20,30,40,50,60,70,80,90]);
    uni1=unique(x1(find(x1(:,9)>=q1(1,6)&x1(:,9)<q1(1,7)),1)); 
    for i=1:size(uni1,1)
        abc=x1(find(x1(:,1)==uni1(i,1)),:);
        ab=horzcat(abc,7);
        RankONE=vertcat(RankONE,ab);
    end
    rank7=vertcat(rank7,RankONE);
end

save rank7 rank7
clear all   %清除workspace
clc  
tic  

%% MAX分組8
load RETall
RETall(:,9)=RETall(:,9)./100;
rank8=[];
Date=unique(RETall(:,2));
for D=1:size(Date,1)
    x1=RETall(find(RETall(:,2)==Date(D,1)),:); %抓出其中一個月份
    
    RankONE=[];
    q1=prctile(x1(:,9),[10,20,30,40,50,60,70,80,90]);
    uni1=unique(x1(find(x1(:,9)>=q1(1,7)&x1(:,9)<q1(1,8)),1)); 
    for i=1:size(uni1,1)
        abc=x1(find(x1(:,1)==uni1(i,1)),:);
        ab=horzcat(abc,8);
        RankONE=vertcat(RankONE,ab);
    end
    rank8=vertcat(rank8,RankONE);
end

save rank8 rank8
clear all   %清除workspace
clc  
tic  

%% MAX分組9
load RETall
RETall(:,9)=RETall(:,9)./100;
rank9=[];
Date=unique(RETall(:,2));
for D=1:size(Date,1)
    x1=RETall(find(RETall(:,2)==Date(D,1)),:); %抓出其中一個月份
    
    RankONE=[];
    q1=prctile(x1(:,9),[10,20,30,40,50,60,70,80,90]);
    uni1=unique(x1(find(x1(:,9)>=q1(1,8)&x1(:,9)<q1(1,9)),1)); 
    for i=1:size(uni1,1)
        abc=x1(find(x1(:,1)==uni1(i,1)),:);
        ab=horzcat(abc,9);
        RankONE=vertcat(RankONE,ab);
    end
    rank9=vertcat(rank9,RankONE);
end

save rank9 rank9
clear all   %清除workspace
clc  
tic  

%% MAX分組10(高)
load RETall
RETall(:,9)=RETall(:,9)./100;
rank10=[];
Date=unique(RETall(:,2));
for D=1:size(Date,1)
    x1=RETall(find(RETall(:,2)==Date(D,1)),:); %抓出其中一個月份
    
    RankONE=[];
    q1=prctile(x1(:,9),[10,20,30,40,50,60,70,80,90]);
    uni1=unique(x1(find(x1(:,9)>=q1(1,9)),1)); 
    for i=1:size(uni1,1)
        abc=x1(find(x1(:,1)==uni1(i,1)),:);
        ab=horzcat(abc,10);
        RankONE=vertcat(RankONE,ab);
    end
    rank10=vertcat(rank10,RankONE);
end

save rank10 rank10
clear all   %清除workspace
clc  
tic  

%% MAX與報酬率和動能
%3.SIZE 4.LEVERAGE 5.BM Ratio 6.IVOL 7.momemtum 8.Illiq 9.MAX
%10.ASVI 11.RET 12.Price 13.Price(t+1) 14.RET(t+1) 15.MOM(t+1) 16.Rank
load rank1
load rank2
load rank3
load rank4
load rank5
load rank6
load rank7
load rank8
load rank9
load rank10

result1=horzcat(1,mean((rank1(:,11)./100)),mean(rank1(:,14)),mean(rank1(:,7)),mean(rank1(:,15))); %2.RET 3.RET(t+1) 4.MOM 5.MOM(t+1)
result2=horzcat(2,mean((rank2(:,11)./100)),mean(rank2(:,14)),mean(rank2(:,7)),mean(rank2(:,15))); %2.RET 3.RET(t+1) 4.MOM 5.MOM(t+1)
result3=horzcat(3,mean((rank3(:,11)./100)),mean(rank3(:,14)),mean(rank3(:,7)),mean(rank3(:,15))); %2.RET 3.RET(t+1) 4.MOM 5.MOM(t+1)
result4=horzcat(4,mean((rank4(:,11)./100)),mean(rank4(:,14)),mean(rank4(:,7)),mean(rank4(:,15))); %2.RET 3.RET(t+1) 4.MOM 5.MOM(t+1)
result5=horzcat(5,mean((rank5(:,11)./100)),mean(rank5(:,14)),mean(rank5(:,7)),mean(rank5(:,15))); %2.RET 3.RET(t+1) 4.MOM 5.MOM(t+1)
result6=horzcat(6,mean((rank6(:,11)./100)),mean(rank6(:,14)),mean(rank6(:,7)),mean(rank6(:,15))); %2.RET 3.RET(t+1) 4.MOM 5.MOM(t+1)
result7=horzcat(7,mean((rank7(:,11)./100)),mean(rank7(:,14)),mean(rank7(:,7)),mean(rank7(:,15))); %2.RET 3.RET(t+1) 4.MOM 5.MOM(t+1)
result8=horzcat(8,mean((rank8(:,11)./100)),mean(rank8(:,14)),mean(rank8(:,7)),mean(rank8(:,15))); %2.RET 3.RET(t+1) 4.MOM 5.MOM(t+1)
result9=horzcat(9,mean((rank9(:,11)./100)),mean(rank9(:,14)),mean(rank9(:,7)),mean(rank9(:,15))); %2.RET 3.RET(t+1) 4.MOM 5.MOM(t+1)
result10=horzcat(10,mean((rank10(:,11)./100)),mean(rank10(:,14)),mean(rank10(:,7)),mean(rank10(:,15))); %2.RET 3.RET(t+1) 4.MOM 5.MOM(t+1)
result=vertcat(result1,result2,result3,result4,result5,result6,result7,result8,result9,result10);

R1=(rank1(:,11)./100);
R10=(rank10(:,11)./100); %t期報酬率
r1=rank1(:,14);
r10=rank10(:,14); %t+1期報酬率
M1=rank1(:,7);
M10=rank10(:,7); %t期動能
m1=rank1(:,15);
m10=rank10(:,15); %t+1期動能
rrr=[];
[h,p,ci,stats]=ttest2(R10,R1);
rrr(:,1)=horzcat(mean(R10),size(R10,1),mean(R1),size(R1,1),h,p,stats.tstat);
[h,p,ci,stats]=ttest2(r10,r1);
rrr(:,2)=horzcat(mean(r10),size(r10,1),mean(r1),size(r1,1),h,p,stats.tstat);
[h,p,ci,stats]=ttest2(M10,M1);
rrr(:,3)=horzcat(mean(M10),size(M10,1),mean(M1),size(M1,1),h,p,stats.tstat);
[h,p,ci,stats]=ttest2(m10,m1);
rrr(:,4)=horzcat(mean(m10),size(m10,1),mean(m1),size(m1,1),h,p,stats.tstat);
xlswrite('file.xlsx',rrr);

result(11,:)=result(10,:)-result(1,:);
Result=vertcat(result,horzcat(11,rrr(7,:)));
title={'MAX','Ret(t)','Ret(t+1)','MOM(t)','MOM(t+1)'};
Result=vertcat(title,num2cell(Result));
xlswrite('rankMAX.xlsx',Result);

