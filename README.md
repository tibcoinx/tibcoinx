import "https://github.com/smartcontractkit/openzeppelin-solidity/blob/v2.5.0/contracts/token/ERC20/SafeERC20.sol";

// Tibcoin contract
contract Tibcoin is SafeERC20 {
    string public name = "Tibcoin";
    string public symbol = "TIB";
    uint8 public decimals = 18;
    uint public totalSupply;

    constructor() public {
        totalSupply = 100000000 * (10 ** uint(decimals));
        // Assign all of the initial supply of Tibcoins to the contract creator
        balanceOf[msg.sender] = totalSupply;
    }

    mapping(address => uint) public balanceOf;

    function transfer(address _to, uint _value) public {
        require(balanceOf[msg.sender] >= _value && _value > 0, "Insufficient balance");
        balanceOf[msg.sender] -= _value;
        balanceOf[_to] += _value;
    }
}