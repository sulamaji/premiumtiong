--DONASI
--BTC:
--35SdKoTnf3uPQmhcjMGQ6MmQHoGLftuYMQ

--DOGE:
--D8G4h7GAGD2kcrnME1XaXGmt3FAhWeb6vS

--ETH:
--0xfbc2b09b189e077666bbcbb08c54bc6f8b827a38

--LTC:
--MASBxmN5JcDeRs68TG4hxXzDKtq27yc9d4

-- Target profit 10% otomatis stop
-- JANGAN MERUBAH APAPUN DALAM SCRIPT SELAIN MENGECILKAN BET
chance1    = 70.71
chance2    = 16
chance3    = 19.8
chance4    = 25
chance5    = 28.29
chance6    = 40.24
chance7    = 47.1
chance8    = 66
chance9    = 10
target     = balance*0.1
prebet     = balance/1000000 --TAMBAH 0 UNTUK MENGECILKAN BET AWAL
betfactor  = 0.00001 --BETFACTOR RUBAH DI SINI
basebet    = balance*betfactor   
nextbet    = prebet
chance     = chance5
bethigh    = false
lostchance = 1
losecount  = 0
wincount   = 0
trigger    = 0
betcount   = 0
preroll    = 65
counter    = 0
high       = 0
low        = 0
roll       = 0
iflose1    = 3.5
iflose2    = 1.25
iflose3    = 1.3
iflose4    = 1.38
iflose5    = 1.43
iflose6    = 1.7
iflose7    = 1.8
iflose8    = 2.5
iflose9    = 1.15
resetseed()
p      = 0
startb = balance
currency   = 'doge'
function dobet()

p = balance - startb

loadgun()
betroll()
rstseed()
viewstats()
betcount+=1
roll+=1
if basebet>balance/100000 then -- GANTI BASEBET DI SINI
    basebet = balance/100000 -- GANTI BASEBET DI SINI
end
e=currentstreak+preroll 
if win then
    goal()
    loadgun()
    basebet=balance*betfactor
    if basebet<balance/100000 then -- GANTI BASEBET DI SINI
    basebet = balance/100000 -- GANTI BASEBET DI SINI
    end
    nextbet=prebet
    wincount+=1
    losecount=0
    hilo()
    if trigger==1 then
        chance     = chance1
        lostchance = 1
        preroll    = 4 --70.71 --3.5
    end
    if trigger==2 then
        chance     = chance2
        lostchance = 2
        preroll    = 25 --16 --1.25
    end
    if trigger==3 then
        chance     = chance3
        lostchance = 3
        preroll    = 16 --19.8 --1.3
    end
    if trigger==4 then
        chance     = chance4
        lostchance = 4
        preroll    = 15 --25 --1.38
    end
    if trigger==5 then
        chance     = chance5
        lostchance = 5
        preroll    = 9 --28.29 --1.43
    end
    if trigger==6 then
        chance     = chance6
        lostchance = 6
        preroll    = 8 --40.24 --1.7
    end
    if trigger==7 then
        chance     = chance7
        lostchance = 7
        preroll    = 6 --47.1 --1.8
    end
    if trigger==8 then
        chance     = chance8
        lostchance = 8
        preroll    = 5 --66 --2.5
    end
    if trigger==9 then
        chance     = chance9
        lostchance = 9
        preroll    = 40 --10 --1.1
    end
else
    losecount+=1
    nexbet=prebet

    if lostchance==1 then
    randomizer()
        if e == 0 then  
            chance=chance1
            nextbet=basebet
        end
        if e <0 then
            chance=chance1
            nextbet=previousbet*iflose1
        end     
    end
    if lostchance==2 then
        if e == 0 then  
            chance=chance2
            nextbet=basebet
        end
        if e <0 then
            chance=chance2
            nextbet=previousbet*iflose2
        end
    end
        if lostchance==3 then
        if e == 0 then  
            chance=chance3
            nextbet=basebet
        end
        if e <0 then
            chance=chance3
            nextbet=previousbet*iflose3
        end
    end
    if lostchance==4 then
        if e == 0 then  
            chance=chance4
            nextbet=basebet
        end
        if e <0 then
            chance=chance4
            nextbet=previousbet*iflose4
        end
    end
    if lostchance==5 then
        -- randomizer()
        if e == 0 then  
            chance=chance5
            nextbet=basebet
        end
        if e <0 then
            chance=chance5
            nextbet=previousbet*iflose5
        end
    end
    if lostchance==6 then
        if e == 0 then  
            chance=chance6
            nextbet=basebet
        end
        if e <0 then
            chance=chance6
            nextbet=previousbet*iflose6
        end     
    end
    if lostchance==7 then
            if e == 0 then  
            chance=chance7
            nextbet=basebet
        end
        if e <0 then
            chance=chance7
            nextbet=previousbet*iflose7
        end     
    end
    if lostchance==8 then
    randomizer()
        if e == 0 then  
            chance=chance8
            nextbet=basebet
        end
        if e <0 then
            chance=chance8
            nextbet=previousbet*iflose8
        end     
    end
    if lostchance==9 then
        if e == 0 then  
            chance=chance9
            nextbet=basebet
        end

        if e <0 then
            chance=chance9
            nextbet=previousbet*iflose9
        end     
    end
end
end
function hilo()
        if high > low then
    bethigh=true
        else
    bethigh=false
        end
       if (high-low) > 5 then
    bethigh=false
        end
        if (low-high)> 5 then
    bethigh=true
        end
end
function betroll()
    if (lastBet.roll < chance) then
        low += 1
    end
    if (lastBet.roll > (99.99 - chance)) then
        high += 1
    end 
end
function rstseed()

if counter==500 then

    resetseed()
    counter=0
    low=0
    high=0
else
    counter+=1
end
end
function viewstats()
print(" ") 
print("Jumlah Total Bet: "..betcount)
print("Jumlah total kalah : "..losecount)
print("Jumlah total menang : "..wincount)
print("Kalah : "..(betcount-wincount))
print("Total profit : "..string.format("%.8f",profit))
print("Stop Profit : "..string.format("%.8f",target))
print("Total Balance : "..string.format("%.8f",balance))
print("High :"..high.." / ".."Low :"..low)
print(" ")
end
function randomizer()
r=math.random(10)
if r>5 then
    bethigh=true
else
    bethigh=false
end
end
function loadgun()
t=math.random(9)

    trigger=t
end
function goal()
if profit>target then
    stop()
    print(" ")
    print("Total!!!")
    print(" ")
    print("Jumlah Wins : "..wincount)
    print("Jumlah Losses : "..(betcount-wincount))
    print("Total Bet : "..betcount)
    print("Profit : "..string.format("%.8f",profit))
    print("Stop : "..string.format("%.8f",target))
    print("Balance : "..string.format("%.8f",balance))
    print(" ")
else
end
end