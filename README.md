# Blockchain-based-Intellectual-Property-Licensing
Use smart contracts to automate the licensing and royalty distribution process for intellectual property, such as patents and trademarks.
# Import necessary libraries
from dataclasses import dataclass
from typing import List, Dict

# Define a basic structure for Smart Contract, Intellectual Property, and Transactions
@dataclass
class IntellectualProperty:
    ip_id: str
    owner: str
    license_fee: float  # Licensing fee to use the IP

@dataclass
class LicenseAgreement:
    contract_id: str
    ip_id: str
    licensee: str
    license_fee: float

@dataclass
class Transaction:
    transaction_id: str
    from_address: str
    to_address: str
    amount: float
    contract_id: str

# Blockchain simulation
class BlockchainSimulator:
    def __init__(self):
        self.ips: Dict[str, IntellectualProperty] = {}  # Registered IPs
        self.contracts: Dict[str, LicenseAgreement] = {}  # Active license agreements
        self.transactions: List[Transaction] = []  # Transactions (royalty distributions)

    def register_ip(self, ip: IntellectualProperty):
        self.ips[ip.ip_id] = ip
        print(f"IP Registered: {ip.ip_id} by {ip.owner}")

    def create_license_agreement(self, ip_id: str, licensee: str, contract_id: str):
        if ip_id in self.ips:
            ip = self.ips[ip_id]
            agreement = LicenseAgreement(contract_id, ip_id, licensee, ip.license_fee)
            self.contracts[contract_id] = agreement
            print(f"License Agreement Created: {contract_id} for IP {ip_id} with {licensee}")
        else:
            print("IP not registered.")

    def execute_transaction(self, transaction: Transaction):
        if transaction.contract_id in self.contracts:
            self.transactions.append(transaction)
            print(f"Transaction Executed: {transaction.transaction_id} from {transaction.from_address} to {transaction.to_address} for ${transaction.amount}")
        else:
            print("Invalid contract ID for transaction.")

# Example usage
if __name__ == "__main__":
    # Initialize blockchain simulator
    blockchain = BlockchainSimulator()

    # Register some IPs
    ip1 = IntellectualProperty("IP001", "Alice", 100.0)
    blockchain.register_ip(ip1)

    # Create a license agreement
    blockchain.create_license_agreement("IP001", "Bob", "CONTRACT001")

    # Simulate a transaction (license fee payment)
    transaction1 = Transaction("TX001", "Bob", "Alice", 100.0, "CONTRACT001")
    blockchain.execute_transaction(transaction1)
