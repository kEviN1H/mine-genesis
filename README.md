# How To Mine Your Genesis Block

In src/chainparams.cpp you need to add some code to create the genesis.

Add this near consensus.powlimit =

	bool CheckProofOfWork(uint256 hash, unsigned int nBits, const Consensus::Params&);
  
Add the actual miner under consensus.hashGenesisBlock = AND don't forget to change the nonce.

	uint32_t nNonce; 
        for(nNonce = 0; ; nNonce++){ 
        genesis.nNonce = nNonce; 
        // You can also update genesis.nTime 
 
        if (CheckProofOfWork(genesis.GetHash(), genesis.nBits, consensus)) { 
            printf("hash: %s\n", genesis.GetHash().GetHex().c_str()); 
            printf("nonce: %i\n", nNonce); 
	    printf("merkle: %s\n", genesis.hashMerkleRoot.ToString().c_str());
            printf("nTime: %u \n", genesis.nTime);
	    printf("V: %u \n", genesis.nVersion);
            break; 
        	} 
 
        if (nNonce == 0) { 
            printf("Can't find a valid nNonce.\n"); 
            break; 
        	} 
    	}

Also you need to add 

	#include <pow.h>
	
Compile and youll recieve and error the first time you load up. Copy all hash, genesis and nonce and update your chainparams.cpp file.
