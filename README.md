algebric
a=[2 3 -1 4; 1 -2 6 -7]
b=[8; -3]
c=[2 3 4 7]
n=4;
m=2;
if(n>m)
    ncm=nchoosek(n,m);
    pair=nchoosek(1:n,m);
    sol=[];

    for i=1:ncm
        y=zeros(n,1);
        x=a(:,pair(i,:))\b
        if all(x>=0 & x~=inf & x~=-inf)
            y(pair(i,:))=x
            sol=[sol,y]
        end
    end
else
    error('ncm not exist');
end
z=c*sol
[zmax zindex]=max(z)
ans=sol(:,zindex) 


graphical
a=[-3 4; 2 -2]
b=[12 ; -2]
c=[1 -3]
x1=0:1:max(b)
x21=(b(1)-(a(1,1)*x1))/a(1,2)
x22=(b(2)-(a(2,1)*x1))/a(2,2)
x21=max(0,x21)
x22=max(0,x22)
% plot(x1,x21,'r',x1,x22,'b')

% inter
pt=[0;0]
for i=1:size(a,1)
    a1=a(i,:)
    b1=b(i,:)
    for j=i+1:size(a,1)
        a2=a(j,:)
        b2=b(j,:)
        a4=[a1;a2]
        b4=[b1;b2]
        x=a4\b4
        pt=[pt x]
    end
end
points=pt'
p=unique(points,"rows")

b1=p(:,1)
b2=p(:,2)
const1=round((-3*b1)+(4*b2)-12)
s1=find(const1>0)
p(s1,:)=[]

b1=p(:,1)
b2=p(:,2)
const2=round((2*b1)+(-2*b2)+2)
s2=find(const2>0)
p(s2,:)=[]

b1=p(:,1)
b2=p(:,2)
const3=round(-b1)
s3=find(const3>0)
p(s3,:)=[]

b1=p(:,1)
b2=p(:,2)
const4=round(-b2)
s4=find(const4>0)
p(s4,:)=[]

feasible=p

% value
for i=1:size(p,1)
    fn(i,:)=sum(p(i,:).*c)
    optimal=min(fn)
end
index=find((optimal-fn)==0)
ans=p(index,:)
