# ASVI
Calculate ASVI(Abnormal Search Volume Index) of the listed companies in Taiwan using Matlab
%%
%Part I ASVI
% AVGSVI 
%%計算svi前12個月的平均值以及標準差
SVI=xlsread('C:\Users\gg90180\Desktop\論文\Data\SVI.xlsx')
AVGSVIall=[]; %AVGSVI of all firms
corID=unique(SVI(:,1));
for id=1:size(corID,1)
     iiD=SVI(find(SVI(:,1)==corID(id,1)),:);
     
     iiDavgsviAll=[]; %AVGSVI of each firm
     [qn,qv]=size(iiD);
     for t=13:size(iiD,1);
         iiD12=iiD(t-12:t-1,:);
         iiDavgsvi=horzcat(iiD(t,[1,2]),mean(iiD12(:,qv)),std(iiD12(:,qv)));
         iiDavgsviAll=vertcat(iiDavgsviAll,iiDavgsvi); 
     end
     AVGSVIall=vertcat(AVGSVIall, iiDavgsviAll); % AVGSVI of all firms
end
AVGSVItitle={'CorID','Date','AVGSVI','STDSVI'}
AVGSVIresults=vertcat(AVGSVItitle,num2cell(AVGSVIall));
xlswrite('C:\Users\gg90180\Desktop\論文\Data\AVGSVI.xlsx', AVGSVIresults);

%% Part II Converge
%converge to SVIdata
%%將前述資料併入SVI資料裡面
SVI=xlsread('C:\Users\gg90180\Desktop\論文\Data\SVI.xlsx');
AVGSVI=xlsread('C:\Users\gg90180\Desktop\論文\Data\AVGSVI.xlsx');
SVI=horzcat(SVI(:,2)*10000+SVI(:,1),SVI);
AVGSVI=horzcat(AVGSVI(:,2)*10000+AVGSVI(:,1),AVGSVI);
for i=1:size(SVI,1)
    b=find(SVI(i,1)==AVGSVI(:,1)); %將SVI併入AVGSVI
    AVGSVI(b,6)=SVI(i,4); 
end
AVGSVI(:,1)=[];
AVGSVItitle={'CorID','Date','AVGSVI','SDSVI','SVI'}
AVGSVIresults=vertcat(AVGSVItitle,num2cell(AVGSVI));
xlswrite('C:\Users\gg90180\Desktop\論文\Data\SVIdata.xlsx', AVGSVIresults);

%% Part III Calculate ASVI
%計算ASVI=(SVI-AVGSVI)/SDSVI
SVIdata=xlsread('C:\Users\gg90180\Desktop\論文\Data\SVIdata.xlsx');
SVIdata=horzcat(SVIdata,((SVIdata(:,5)-SVIdata(:,3))./SVIdata(:,4)));
SVIdatatitle={'CorID','Date','AVGSVI','SDSVI','SVI','ASVI'}
SVIdataresults=vertcat(SVIdatatitle,num2cell(SVIdata));
xlswrite('C:\Users\gg90180\Desktop\論文\Data\ASVI.xlsx', SVIdataresults);
