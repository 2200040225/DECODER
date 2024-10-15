Design code:


module decoder24 (
    input [1:0] in,   
    input en,         
    output reg [3:0] out
);

always @(*)
begin
    if (en) 
    begin
        case (in)
            2'b00: out = 4'b0001;
            2'b01: out = 4'b0010;
            2'b10: out = 4'b0100;
            2'b11: out = 4'b1000;
            default: out = 4'b0000;
        endcase
    end 
    else
    begin
        out = 4'b0000; 
    end
end

endmodule

Test bench :

module decoder24_tb();
reg [1:0] in;
reg en;
wire [3:0] out;
decoder24 uut (
    .in(in), 
    .en(en), 
    .out(out)
);

initial begin
    en = 0;
    in = 2'b00;
    #10;
    en = 1; 
    in = 2'b00;  
    #10; 
    in = 2'b01;         
    #10; 
    in = 2'b10;          
    #10; 
    in = 2'b11;         
    #10; en = 0; in = 2'b00;  
    #10; en = 1; in = 2'b00;  
    #10; 
    $finish();           
end
initial begin
    $monitor("Time = %0t, Enable = %b, Input = %b, Output = %b", $time, en, in, out);
end
endmodule
