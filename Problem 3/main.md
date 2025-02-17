interface WalletBalance {
    currency: string;
    amount: number;
    blockchain: string;
}

interface FormattedWalletBalance extends WalletBalance {
    formatted: string;
}

interface Props extends BoxProps {}

const blockchainPriority: Record<string, number> = {
    Osmosis: 100,
    Ethereum: 50,
    Arbitrum: 30,
    Zilliqa: 20,
    Neo: 20,
};

const getPriority = (blockchain: string): number => {
    return blockchainPriority[blockchain] ?? -99;
};

const WalletPage: React.FC<Props> = (props) => {
    const { children, ...rest } = props;
    const balances = useWalletBalances();
    const prices = usePrices();

    const sortedBalances = useMemo(() => {
        return balances
            .filter((balance) => getPriority(balance.blockchain) > -99 && balance.amount > 0)
            .sort((a, b) => getPriority(b.blockchain) - getPriority(a.blockchain));
    }, [balances]);

    const rows = sortedBalances.map((balance) => {
        const formattedBalance: FormattedWalletBalance = {
            ...balance,
            formatted: balance.amount.toFixed(),
        };
        const usdValue = prices[balance.currency] * balance.amount;

        return (
            <WalletRow
                className={classes.row}
                key={balance.currency} // Using a stable key
                amount={balance.amount}
                usdValue={usdValue}
                formattedAmount={formattedBalance.formatted}
            />
        );
    });

    return <div {...rest}>{rows}</div>;
};



//
Fixed lhsPriority bug (now correctly referencing balancePriority).
Refactored getPriority() to avoid redundant calls (uses a dictionary lookup).
Removed unnecessary .filter() inside sorting.
Reduced double-mapping by combining formatting into the .map() loop.
Used a stable key (balance.currency) for list rendering.
Fixed incorrect types (blockchain: any → string).
Optimized useMemo() dependencies (removed unnecessary prices dependency).
//
