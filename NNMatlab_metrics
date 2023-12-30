net_h= @(i1,i2,w_11,w_21) i1*w_11+i2*w_21;
net_o= @(h1,h2,h3,h4,w_11,w_21,w_31,w_41)h1*w_11+h2*w_21+h3*w_31+h4*w_41;
f=@(x)(exp(2*x)-1)/(exp(2*x)+1);
f_deriv=@(x) 1/ (cosh(x)^2);
back_out=@(out,target,f_deriv_net,out_hi) (out-target)*f_deriv_net*out_hi;
back_hidden=@(out,target,f_deriv_net,w_j1,i_i) (out-target)*w_j1*f_deriv_net*i_i;
w_hidden=rand(2,4);
w_out=rand(1,4);
eta=0.17;
sum=0;
nr=0;
input=rand(10000,2);
for i=1:10000
    if input(i,1) > 0.5
        out(i)=1;
    else
        out(i)=0;
    end
end


for i=1:10000
    %forword pass
    net_h_1=net_h(input(i,1),input(i,2),w_hidden(1,1),w_hidden(2,1));
    net_h_2=net_h(input(i,1),input(i,2),w_hidden(1,2),w_hidden(2,2));
    net_h_3=net_h(input(i,1),input(i,2),w_hidden(1,3),w_hidden(2,3));
    net_h_4=net_h(input(i,1),input(i,2),w_hidden(1,4),w_hidden(2,4));
    
    out_h_1=f(net_h_1);
    out_h_2=f(net_h_2);
    out_h_3=f(net_h_3);
    out_h_4=f(net_h_4);

    net_o_1=net_o(out_h_1,out_h_2,out_h_3,out_h_4,w_out(1,1),w_out(1,2),w_out(1,3),w_out(1,4));
    
    out_o_1=f(net_o_1);
    
    %if out_o_1 > 0.5
    %    out_o_1=1;
    %else
    %    out_o_1=0;
    %end
    %backward pass
    f_derivv =f_deriv(net_o_1);
    %f_derivv = out_o_1*(1-out_o_1);
    
    back_out_1= back_out(out_o_1,out(i),f_derivv,out_h_1);
    back_out_2=back_out(out_o_1,out(i),f_derivv,out_h_2);
    back_out_3=back_out(out_o_1,out(i),f_derivv,out_h_3);
    back_out_4=back_out(out_o_1,out(i),f_derivv,out_h_4);
    
    w_out(1,1) = w_out(1,1) - eta*back_out_1;
    w_out(1,2) = w_out(1,2) - eta*back_out_2;
    w_out(1,3) = w_out(1,3) - eta*back_out_3;
    w_out(1,4) = w_out(1,4) - eta*back_out_4;
    
    
    f_deriv_h1=f_deriv(net_h_1);
    f_deriv_h2=f_deriv(net_h_2);
    f_deriv_h3=f_deriv(net_h_3);
    f_deriv_h4=f_deriv(net_h_4);
    
    %f_deriv_h1 = out_h_1*(1-out_h_1);
    %f_deriv_h2 = out_h_2*(1-out_h_2);
    %f_deriv_h3 = out_h_3*(1-out_h_3);
    %f_deriv_h4 = out_h_4*(1-out_h_4);
    
    back_hidd_1_1 = back_hidden(out_o_1,out(i),f_deriv_h1,w_out(1,1),input(i,1));
    back_hidd_1_2 = back_hidden(out_o_1,out(i),f_deriv_h2,w_out(1,2),input(i,1));
    back_hidd_1_3 = back_hidden(out_o_1,out(i),f_deriv_h3,w_out(1,3),input(i,1));
    back_hidd_1_4 = back_hidden(out_o_1,out(i),f_deriv_h4,w_out(1,4),input(i,1));
  
    back_hidd_2_1 = back_hidden(out_o_1,out(i),f_deriv_h1,w_out(1,1),input(i,2));
    back_hidd_2_2 = back_hidden(out_o_1,out(i),f_deriv_h2,w_out(1,2),input(i,2));
    back_hidd_2_3 = back_hidden(out_o_1,out(i),f_deriv_h3,w_out(1,3),input(i,2));
    back_hidd_2_4 = back_hidden(out_o_1,out(i),f_deriv_h4,w_out(1,4),input(i,2));
    
    w_hidden(1,1) = w_hidden(1,1) - eta*back_hidd_1_1;
    w_hidden(1,2) = w_hidden(1,2) - eta*back_hidd_1_2;
    w_hidden(1,3) = w_hidden(1,3) - eta*back_hidd_1_3;
    w_hidden(1,4) = w_hidden(1,4) - eta*back_hidd_1_4;
    
    w_hidden(2,1) = w_hidden(2,1) - eta*back_hidd_2_1;
    w_hidden(2,2) = w_hidden(2,2) - eta*back_hidd_2_2;
    w_hidden(2,3) = w_hidden(2,3) - eta*back_hidd_2_3;
    w_hidden(2,4) = w_hidden(2,4) - eta*back_hidd_2_4;
    some =abs(out_o_1 - out(i));
    %if some < 0.5
    %    nr = nr+1;
    %    sum=sum + some;
    %end
    %plot(i,some,'x')
    %hold on
end
%sum=sum/nr;
%sum

a=0;
b=0;
c=0;
d=0;


input=rand(1000,2);
for i=1:1000
    if input(i,1) > 0.5
        out1(i)=1;
    else
        out1(i)=0;
    end
end

%plot(input(:,1),input(:,2),'x')

for i=1:1000
    %forword pass
    net_h_1=net_h(input(i,1),input(i,2),w_hidden(1,1),w_hidden(2,1));
    net_h_2=net_h(input(i,1),input(i,2),w_hidden(1,2),w_hidden(2,2));
    net_h_3=net_h(input(i,1),input(i,2),w_hidden(1,3),w_hidden(2,3));
    net_h_4=net_h(input(i,1),input(i,2),w_hidden(1,4),w_hidden(2,4));
    
    out_h_1=f(net_h_1);
    out_h_2=f(net_h_2);
    out_h_3=f(net_h_3);
    out_h_4=f(net_h_4);

    net_o_1=net_o(out_h_1,out_h_2,out_h_3,out_h_4,w_out(1,1),w_out(1,2),w_out(1,3),w_out(1,4));
    
    out_o_1=f(net_o_1);
    if out_o_1 > 0.5
        if out1(i) ==1
            a=a+1;
        else
            b=b+1;
        end
    else
         if out1(i) ==1   
            c=c+1;
         else
             d=d+1;
         end
    end
    sensitivty1=a/(a+c);
    specifilty1 = d/(b+d);
    %ROC curve
    %plot(sensitivty1,(1-specifilty1),'.')
    %xlim([0 1])
    %ylim([0 1])
    %hold on
    some =(out_o_1 - out1(i))^2;
    if some == 0
        %nothing
    else
        nr = nr+1;
    end
    sum=sum + some;
    %end
    %plot(i,some,'.')
    %hold on
end
sum =sum/1000;
RSME= sqrt(sum)
accuracy=(a+d)/(a+b+c+d)
precision =a/(a+b)
sensitivty=a/(a+c)
specifilty = d/(b+d)
negative_predicted_value = d/(c+d)

F_1_Score = 2*(precision*sensitivty)/(precision+sensitivty)


