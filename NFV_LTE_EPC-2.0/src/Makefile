#---------------Final Target----------------#

all:	hss.out mme.out pgw.out ransim.out sgw.out sink.out

#-------------------------------------------#


#-----------------Compiler------------------#

G++ = g++ -std=c++0x -std=c++11 -O3 -std=gnu++0x -ggdb -I./client -Wno-deprecated -fpermissive -w

#----please use appropriate LIB flag for different data stores
LIB = -lkvstore -lkvs_redis  
#LIB = -lkvstore -lkvs_leveldb
#LIB = -lkvstore -lkvs_memcached -lmemcached
PATH_TO_RAMCLOUD = ../../KeyValueStore/Implementation/RAMCloud/RAMCloud/obj.master/
#LIB = -L$(PATH_TO_RAMCLOUD) -lkvstore -lkvs_ramcloud -lramcloud -lprotobuf -lpcrecpp -lboost_system -lzookeeper_mt


#-------------------------------------------#


#---------------Object files----------------#

diameter.o:	diameter.cpp diameter.h utils.h
	$(G++) -c -o diameter.o diameter.cpp

gtp.o:	gtp.cpp gtp.h utils.h
	$(G++) -c -o gtp.o gtp.cpp

hss.o:	diameter.h gtp.h hss.cpp hss.h  network.h packet.h s1ap.h sctp_server.h sync.h utils.h
	$(G++) -c -o  hss.o hss.cpp -Wno-deprecated -lboost_serialization

hss_server.o:	diameter.h gtp.h hss.h hss_server.cpp hss_server.h network.h packet.h s1ap.h sctp_server.h sync.h utils.h
	$(G++) -c -o hss_server.o hss_server.cpp	

mme.o:	diameter.h gtp.h mme.cpp mme.h network.h packet.h s1ap.h sctp_client.h sctp_server.h security.h sync.h telecom.h udp_client.h udp_server.h utils.h
	$(G++) -c -o mme.o mme.cpp -Wno-deprecated -lboost_serialization

mme_server.o:	diameter.h gtp.h mme.h mme_server.cpp mme_server.h network.h packet.h s1ap.h sctp_client.h sctp_server.h security.h sync.h telecom.h udp_server.h udp_client.h utils.h
	$(G++) -c -o mme_server.o mme_server.cpp	

network.o:	diameter.h gtp.h network.cpp network.h packet.h s1ap.h utils.h 
	$(G++) -c -o network.o network.cpp

packet.o:	diameter.h gtp.h packet.cpp packet.h s1ap.h utils.h
	$(G++) -c -o packet.o packet.cpp

pgw.o:	diameter.h gtp.h network.h packet.h pgw.cpp pgw.h s1ap.h sync.h udp_client.h udp_server.h utils.h
	$(G++) -c -o pgw.o pgw.cpp -Wno-deprecated -lboost_serialization -lkvstore

pgw_server.o:	diameter.h gtp.h network.h packet.h pgw.h pgw_server.cpp pgw_server.h s1ap.h sync.h udp_client.h udp_server.h utils.h
	$(G++) -c -o pgw_server.o pgw_server.cpp -Wno-deprecated -lboost_serialization -lkvstore

ran.o:	diameter.h gtp.h network.h packet.h ran.cpp ran.h s1ap.h sctp_client.h security.h sync.h telecom.h tun.h udp_client.h udp_server.h utils.h
	$(G++) -c -o ran.o ran.cpp

ran_simulator.o:	diameter.h gtp.h network.h packet.h ran.h ran_simulator.cpp ran_simulator.h s1ap.h sctp_client.h security.h sync.h telecom.h tun.h udp_client.h udp_server.h utils.h
	$(G++) -c -o ran_simulator.o ran_simulator.cpp

s1ap.o:	s1ap.cpp s1ap.h utils.h
	$(G++) -c -o s1ap.o s1ap.cpp

sctp_client.o:	diameter.h gtp.h network.h packet.h s1ap.h sctp_client.cpp sctp_client.h utils.h
	$(G++) -c -o sctp_client.o sctp_client.cpp

sctp_server.o:	diameter.h gtp.h network.h packet.h s1ap.h sctp_server.cpp sctp_server.h sync.h utils.h
	$(G++) -c -o sctp_server.o sctp_server.cpp	

security.o:	diameter.h gtp.h packet.h s1ap.h security.cpp security.h utils.h
	$(G++) -c -o security.o security.cpp

sgw.o:	diameter.h gtp.h network.h packet.h s1ap.h sgw.cpp sgw.h sync.h udp_client.h udp_server.h utils.h
	$(G++) -c -o sgw.o sgw.cpp -lboost_serialization -lkvstore

sgw_server.o:	diameter.h gtp.h network.h packet.h s1ap.h sgw.h sgw_server.cpp sgw_server.h sync.h udp_client.h udp_server.h utils.h
	$(G++) -c -o sgw_server.o sgw_server.cpp 

sink.o:	diameter.h gtp.h network.h packet.h s1ap.h sink.cpp sink.h tun.h udp_client.h udp_server.h utils.h
	$(G++) -c -o sink.o sink.cpp

sink_server.o:	diameter.h gtp.h network.h packet.h s1ap.h sink.h sink_server.cpp sink_server.h tun.h udp_client.h udp_server.h utils.h
	$(G++) -c -o sink_server.o sink_server.cpp	

sync.o:	sync.cpp sync.h utils.h
	$(G++) -c -o sync.o sync.cpp

telecom.o:	telecom.cpp telecom.h utils.h
	$(G++) -c -o telecom.o telecom.cpp

tun.o:	diameter.h gtp.h network.h packet.h s1ap.h tun.cpp tun.h utils.h
	$(G++) -c -o tun.o tun.cpp

udp_client.o:	diameter.h gtp.h network.h packet.h s1ap.h udp_client.cpp udp_client.h utils.h
	$(G++) -c -o udp_client.o udp_client.cpp

udp_server.o:	diameter.h gtp.h network.h packet.h s1ap.h udp_server.cpp udp_server.h utils.h
	$(G++) -c -o udp_server.o udp_server.cpp

utils.o:	utils.cpp utils.h
	$(G++) -c -o utils.o utils.cpp

#-------------------------------------------#


#---------Prerequisites and Recipes---------#

HSS_P = diameter.o gtp.o hss.o hss_server.o  network.o packet.o s1ap.o sctp_server.o sync.o utils.o
HSS_R = $(G++) -o hss.out $(HSS_P) -pthread -lboost_serialization -Wno-deprecated $(LIB)

MME_P = diameter.o gtp.o mme.o mme_server.o network.o packet.o s1ap.o sctp_client.o sctp_server.o security.o sync.o telecom.o udp_client.o udp_server.o  utils.o
MME_R = $(G++) -o mme.out $(MME_P) -pthread -lcrypto -lboost_serialization -Wno-deprecated $(LIB)

PGW_P = diameter.o gtp.o network.o packet.o pgw.o pgw_server.o s1ap.o sync.o udp_client.o udp_server.o utils.o
PGW_R = $(G++) -o pgw.out $(PGW_P) -pthread -Wno-deprecated -lboost_serialization $(LIB)

RAN_P = diameter.o gtp.o network.o packet.o ran.o ran_simulator.o s1ap.o sctp_client.o security.o sync.o telecom.o tun.o udp_client.o udp_server.o utils.o
RAN_R = $(G++) -o ransim.out $(RAN_P) -pthread -lcrypto -lboost_serialization 

SGW_P = diameter.o gtp.o network.o packet.o s1ap.o sgw.o sgw_server.o sync.o udp_client.o udp_server.o utils.o
SGW_R = $(G++) -o sgw.out $(SGW_P) -pthread -lboost_serialization -lboost_serialization $(LIB)

SINK_P = diameter.o gtp.o network.o packet.o s1ap.o sink.o sink_server.o tun.o udp_client.o udp_server.o utils.o
SINK_R = $(G++) -o sink.out $(SINK_P) -pthread -lboost_serialization 

#-------------------------------------------#


#---------------Executable files------------#

hss.out:	$(HSS_P)
	$(HSS_R)

mme.out:	$(MME_P)
	$(MME_R)

pgw.out:	$(PGW_P)
	$(PGW_R)

ransim.out:	$(RAN_P)
	$(RAN_R)

sgw.out:	$(SGW_P)
	$(SGW_R)

sink.out:	$(SINK_P)	
	$(SINK_R)	

#-------------------------------------------#


#------------------Cleaner------------------#

clean:
	rm -f *~ *.o *.out

#-------------------------------------------#


#--------------Special Commands-------------#

# make -k (To keep going on even after encountering errors in making a former target)

#-------------------------------------------#
