import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Table, TableHeader, TableRow, TableHead, TableBody, TableCell } from "@/components/ui/table";
import { Dialog, DialogTrigger, DialogContent } from "@/components/ui/dialog";

export default function CryptoMarketplace() {
  const [listings, setListings] = useState([
    { id: 1, type: "Buy", crypto: "Bitcoin", amount: "0.5 BTC", price: "$30,000", user: "User123" },
    { id: 2, type: "Sell", crypto: "Ethereum", amount: "2 ETH", price: "$3,500", user: "User456" },
  ]);
  const [kycVerified, setKycVerified] = useState(false);
  
  const verifyKYC = () => {
    alert("KYC Verification Submitted. Pending Approval.");
    setKycVerified(true);
  };
  
  return (
    <div className="p-6">
      <h1 className="text-2xl font-bold mb-4">P2P Crypto Marketplace (Nepal-Friendly)</h1>
      <Card className="mb-6">
        <CardContent>
          <p className="text-gray-600">Connect with verified buyers & sellers securely.</p>
        </CardContent>
      </Card>
      
      {!kycVerified && (
        <div className="mb-6">
          <h2 className="text-lg font-semibold">KYC Verification</h2>
          <Input placeholder="Upload ID (Image URL)" className="mb-2" />
          <Button onClick={verifyKYC}>Submit KYC</Button>
        </div>
      )}
      
      <div className="mb-6 flex gap-4">
        <Input placeholder="Search listings..." className="w-full" />
        <Button>Add Listing</Button>
      </div>
      
      <Table>
        <TableHeader>
          <TableRow>
            <TableHead>Type</TableHead>
            <TableHead>Crypto</TableHead>
            <TableHead>Amount</TableHead>
            <TableHead>Price</TableHead>
            <TableHead>User</TableHead>
            <TableHead>Action</TableHead>
          </TableRow>
        </TableHeader>
        <TableBody>
          {listings.map((listing) => (
            <TableRow key={listing.id}>
              <TableCell>{listing.type}</TableCell>
              <TableCell>{listing.crypto}</TableCell>
              <TableCell>{listing.amount}</TableCell>
              <TableCell>{listing.price}</TableCell>
              <TableCell>{listing.user}</TableCell>
              <TableCell>
                <Dialog>
                  <DialogTrigger asChild>
                    <Button variant="outline">Contact</Button>
                  </DialogTrigger>
                  <DialogContent>
                    <h2 className="text-lg font-semibold">Chat with {listing.user}</h2>
                    <Input placeholder="Type your message..." className="mb-2" />
                    <Button>Send</Button>
                  </DialogContent>
                </Dialog>
              </TableCell>
            </TableRow>
          ))}
        </TableBody>
      </Table>
    </div>
  );
}
