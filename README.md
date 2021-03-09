### Preparation Tasks
### 1. Table with connection of 7-segment displays on Nexys A7 board
![Nexys A7](segment.png)
![Nexys A7](segmentsch.png)


### Decoder truth table for common anode 7-segment display
| Hex | Inputs | A | B | C | D | E | F | G |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| 0 | 0000 | 0 | 0 | 0 | 0 | 0 | 0 | 1 |
| 1 | 0001 | 1 | 0 | 0 | 1 | 1 | 1 | 1 |
| 2 | 0010 | 0 | 0 | 1 | 0 | 0 | 1 | 0 |
| 3 | 0011 | 0 | 0 | 0 | 0 | 1 | 1 | 0 |
| 4 | 0100 | 1 | 0 | 0 | 1 | 1 | 0 | 0 |
| 5 | 0101 | 0 | 1 | 0 | 0 | 1 | 0 | 0 |
| 6 | 0110 | 0 | 1 | 0 | 0 | 0 | 0 | 0 |
| 7 | 0111 | 0 | 0 | 1 | 1 | 1 | 1 | 1 |
| 8 | 1000 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 9 | 1001 | 0 | 0 | 0 | 0 | 1 | 0 | 0 |
| A | 1010 | 0 | 0 | 0 | 1 | 0 | 0 | 0 |
| b | 1011 | 1 | 1 | 0 | 0 | 0 | 0 | 0 |
| C | 1100 | 0 | 1 | 1 | 0 | 0 | 0 | 1 |
| d | 1101 | 1 | 0 | 0 | 0 | 0 | 1 | 0 |
| E | 1110 | 0 | 1 | 1 | 0 | 0 | 0 | 0 |
| F | 1111 | 0 | 1 | 1 | 1 | 0 | 0 | 0 |

### 2. Seven-segment display decoder
### Code of hex_7seg.vhdl

a)

```vhdl

architecture Behavioral of hex_7seg is

begin

--------------------------------------------------------------------
    -- p_7seg_decoder:
    -- A combinational process for 7-segment display decoder. 
    -- Any time "hex_i" is changed, the process is "executed".
    -- Output pin seg_o(6) corresponds to segment A, seg_o(5) to B, etc.
    --------------------------------------------------------------------
    p_7seg_decoder : process(hex_i)
    begin
        case hex_i is
            when "0000" =>
                seg_o <= "0000001";     -- num 0
            when "0001" =>
                seg_o <= "1001111";     -- num 1
            when "0010" =>
                seg_o <= "0010010";     -- num 2
            when "0011" =>
                seg_o <= "0000110";     -- num 3
            when "0100" =>
                seg_o <= "1001100";     -- num 4
            when "0101" =>
                seg_o <= "0100100";     -- num 5
            when "0110" =>
                seg_o <= "0100000";     -- num 6
            when "0111" =>
                seg_o <= "0011111";     -- num 7
            when "1000" =>
                seg_o <= "0000000";     -- num 8
            when "1001" =>
                seg_o <= "0000100";     -- num 9
            when "1010" =>
                seg_o <= "0001000";     -- A
            when "1011" =>
                seg_o <= "1100000";     -- B
            when "1100" =>
                seg_o <= "0110001";     -- C
            when "1101" =>
                seg_o <= "1000010";     -- D        
            when "1110" =>
                seg_o <= "0110000";     -- E
            when others =>
                seg_o <= "0111000";     -- F
        end case;
    end process p_7seg_decoder;

end Behavioral;

```

### Code of tb_hex_7seg.vhdl
b)
 ```vhdl
 ----------------------------------------------------------------------------------
-- Company: 
-- Engineer: 
-- 
-- Create Date: 09.03.2021 17:11:29
-- Design Name: 
-- Module Name: tb_hex_7seg - Behavioral
-- Project Name: 
-- Target Devices: 
-- Tool Versions: 
-- Description: 
-- 
-- Dependencies: 
-- 
-- Revision:
-- Revision 0.01 - File Created
-- Additional Comments:
-- 
----------------------------------------------------------------------------------


library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

-- Uncomment the following library declaration if using
-- arithmetic functions with Signed or Unsigned values
--use IEEE.NUMERIC_STD.ALL;

-- Uncomment the following library declaration if instantiating
-- any Xilinx leaf cells in this code.
--library UNISIM;
--use UNISIM.VComponents.all;

entity tb_hex_7seg is
--  Port ( );
end tb_hex_7seg;

architecture Behavioral of tb_hex_7seg is

--Loc. signals

         signal s_hex     : std_logic_vector (4 - 1 downto 0);
         signal s_seg     : std_logic_vector (7 - 1 downto 0);

begin

 uut_hex_7seg : entity work.hex_7seg


          port map (
          hex_i            => s_hex,
          seg_o            => s_seg
          );
          
         p_stimulus : process
         begin
         report "Stimulus process started" severity note;
         
         s_hex <= "0000"; wait for 100ns;
         
         s_hex <= "0001"; wait for 100ns;
         
         s_hex <= "0010"; wait for 100ns;
         
         s_hex <= "0011"; wait for 100ns;
         
         s_hex <= "0100"; wait for 100ns;
         
         s_hex <= "0101"; wait for 100ns;
         
         s_hex <= "0110"; wait for 100ns;
         
         s_hex <= "0111"; wait for 100ns;
         
         s_hex <= "1000"; wait for 100ns;
         
         s_hex <= "1001"; wait for 100ns;
         
         s_hex <= "1010"; wait for 100ns;
         
         s_hex <= "1011"; wait for 100ns;
         
         s_hex <= "1100"; wait for 100ns;
         
         s_hex <= "1101"; wait for 100ns;
         
         s_hex <= "1110"; wait for 100ns;
         
          
         s_hex <= "1111"; wait for 100ns;
         
         --report a note.at the end of stimulus process
         report "Stimulus process finished" severity note;
         wait;
         end process p_stimulus;

end Behavioral;

 ```
 
 
 c) Simulation graphs 
 ![GRAPH](simulation.png)
 
