# Program
Matlab
clear all
X0 = [0.5 0.5];%%receiver's initial strategy
Y0 = [0.5 0.5];%%deceiver's initial strategy




%x = [0.5 0.5];
P0 = 0.8;
P1 = 0.2;
C0 = 0;%% when C = 0, the game will be a cheap talk game C >= 0;
C1 = 0;%%lie under Hypothesis 1
C = 2;
x = [1 0];
y = [1 0];

xp=zeros(1,100);
yp=zeros(1,100);
xp1 =zeros(1,100);
yp1=zeros(1,100);

for n = 1:1:100
%      
%     y(1) = fmincon(@(Y1) Y1*(x(1)+x(2)-1-C0)+2-x(2),0.5,[],[],[],[],0,1);
%     y(2)=  fmincon(@(Y2) Y2*(x(1)+x(2)-C1-1)+C1+1-x(1),0.5,[],[],[],[],0,1);
    y = fmincon(@(Y) Y(1)*(P0*x(1)-P0*(1-x(2))-C*P0)+Y(2)*(P1*x(2)- P1*(1-x(1))-C*P1)+C+1-P0*x(2)-P1*x(1),Y0,[],[],[],[],[0 0],[1 1]);
   yp(n)=y(1);
   yp1(n)= y(2);
   x = fmincon(@(X) X(1)*(P1*(1-y(2)-P0*y(1))) + X(2)*(P0*(1-y(1)) - P1 * y(2)) + P0*y(1) + P1*y(2),X0,[],[],[],[],[0 0],[1 1]);
   xp(n) = x(1);
   xp1(n) = x(2);
    
end 

n1 = 1:1:100;
plot(n1,xp,n1,xp1);
hold on
legend('P(\theta^=0|M=0)','P(\theta^=1|M=1)');

figure
plot(n1,yp,n1,yp1);
hold on
legend('P(M=0|\theta=0)','P(M=1|\theta=1)');
