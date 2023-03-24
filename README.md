# ASVI
Calculate ASVI(Abnormal Search Volume Index) of the listed companies in Taiwan using Matlab
%%
%Part I ASVI
% AVGSVI 
%%Calculate mean and standard deviation of SVI in the past 12 months
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
